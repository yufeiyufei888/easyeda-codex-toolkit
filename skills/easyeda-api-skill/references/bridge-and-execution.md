# Bridge And Execution

Use this reference only for live `eda.*` execution through the bundled bridge.

## Establish The Bridge

1. Scan ports `49620-49629` and accept only a `/health` response whose service is
   `easyeda-bridge`.
2. If no bridge is present, start `scripts/bridge-server.mjs` as a hidden or
   background process, then repeat the identity check.
3. Ensure the `run-api-gateway.eext` extension is installed and loaded in
   EasyEDA when health reports no connected EDA client.

The bridge endpoints are:

- `GET /health`: service identity and connection status.
- `GET /eda-windows`: connected windows and active selection.
- `POST /eda-windows/select`: select `{"windowId":"..."}`.
- `POST /execute`: execute `{"code":"...","windowId":"..."}`; `windowId`
  may be omitted only when one intended active window is unambiguous.

## Select The Exact Context

- Zero windows: stop live execution and report that the extension/client is not
  connected.
- One window: select it and verify current project/document.
- Multiple windows: list them and select the intended one before executing.
- Refresh the list after a disconnect; window identifiers can change after an
  EasyEDA restart.

Before a `SCH_*` or `PCB_*` call, read:

```javascript
const project = await eda.dmt_Project.getCurrentProjectInfo();
const document = await eda.dmt_SelectControl.getCurrentDocumentInfo();
return { project, document };
```

Confirm that a project is open and the document type matches the API domain.
Opening another project can discard unsaved work, so treat it as a scoped state
change and obtain the required authority first.

## Execute

Send code that returns an observable value:

```javascript
return await eda.dmt_Project.getCurrentProjectInfo();
```

For a mutation, use this sequence:

1. Read target primitive/document state.
2. Execute one small documented change.
3. Return the API result.
4. Read the changed state again and compare exact properties.

All API code runs in EasyEDA's browser runtime. Node.js modules such as `fs` and
`path` are unavailable inside the executed function.

## Units And Types

- PCB: 1 coordinate unit = 1 mil = 0.0254 mm.
- Schematic: 1 coordinate unit = 0.01 inch = 10 mil = 0.254 mm.
- Read the exact class signature for parameter order and optional values.
- `await` any `Promise<...>` return.
- Use documented enum members such as `EPCB_LayerId.TOP` instead of raw layer
  numbers.

## Failure Classification

- Bridge absent or wrong service: connection failure.
- No/incorrect active document: document-state failure.
- Method, enum, or parameter mismatch: signature/type failure.
- Documented call consistently rejected: permission failure.
- Browser/DOM/Node primitive used in an extension main process: runtime-context
  failure; use the documented `eda.sys_*` equivalent.
- Method absent from the API references: unsupported API.

**Complete when:** the bridge identity, selected window, project/document state,
exact API signature, returned result, and mutation readback are all recorded.
