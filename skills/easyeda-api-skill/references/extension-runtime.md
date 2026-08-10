# Extension Runtime

Use this reference when writing or debugging an EasyEDA extension.

## Main Process

Use EasyEDA-provided APIs for host interactions:

| Need | Use |
|---|---|
| Text input | `eda.sys_Dialog.showInputDialog()` |
| Selection | `eda.sys_Dialog.showSelectDialog()` |
| Information | `eda.sys_Dialog.showInformationMessage()` |
| Confirmation | `eda.sys_Dialog.showConfirmationMessage()` |
| Toast | `eda.sys_Message.showToastMessage()` |
| Extension settings | `eda.sys_Storage.setExtensionUserConfig()` |
| Custom HTML/UI | `eda.sys_IFrame.openIFrame()` |
| Open URL/window | `eda.sys_Window.open()` |

The extension main process is not a general web page. Put DOM-dependent UI and
browser hardware APIs inside the iframe created by `sys_IFrame`.

## IFrame

- Access the injected EasyEDA API as `eda.*` directly inside the iframe.
- Share persistent data between main process and iframe through
  `eda.sys_Storage`, or call the same documented `eda.*` API from each context.
- Use `window`, `document`, `localStorage`, and browser hardware APIs only inside
  the iframe when the required permissions and product behavior allow them.

Example storage bridge:

```javascript
await eda.sys_Storage.setExtensionUserConfig("key", JSON.stringify(data));
const data = JSON.parse(await eda.sys_Storage.getExtensionUserConfig("key"));
```

## Verification

1. Confirm the code's execution context: main process or iframe.
2. Resolve every host interaction to a documented `eda.sys_*` API.
3. Verify each iframe can access `eda` directly and loads its own DOM/browser
   behavior without reaching through a parent frame.
4. Exercise the extension behavior and record returned values or visible UI.

**Complete when:** every runtime-dependent operation uses the supported context,
main/iframe data exchange is explicit, and the behavior is verified in EasyEDA.
