# API Patterns

Use these as shape examples only after reading the exact current class method,
enum, interface, and remarks.

## Project And Documents

```javascript
return await eda.dmt_Project.getCurrentProjectInfo();
```

```javascript
return await eda.dmt_Board.getAllBoardsInfo();
```

```javascript
await eda.dmt_EditorControl.activateDocument(tabId);
return await eda.dmt_SelectControl.getCurrentDocumentInfo();
```

## Selection

```javascript
return eda.sch_SelectControl.getAllSelectedPrimitives_PrimitiveId();
```

```javascript
return eda.pcb_SelectControl.getAllSelectedPrimitives_PrimitiveId();
```

## Primitive Mutation

Use the documented asynchronous primitive pattern:

```javascript
const primitive = await eda.pcb_PrimitiveVia.get([viaId]);
const change = primitive.toAsync();
change.setState_X(newX);
change.setState_Y(newY);
change.done();
return await eda.pcb_PrimitiveVia.get([viaId]);
```

Confirm the getter return shape in the class reference before selecting an item
or converting it to async form.

## Library

```javascript
return await eda.lib_LibrariesList.getAllLibrariesList();
```

```javascript
return await eda.lib_Device.search("STM32");
```

```javascript
return await eda.lib_Symbol.get(symbolUuid);
```

## DRC

```javascript
return await eda.pcb_Drc.check(true, true, false);
```

The boolean result alone is not a full design report; pair it with the available
violation details and the quality gate used for the board task.

## Completion Criterion

The pattern is ready to use when the current API reference confirms its method
name, parameter order, return shape, units, enums, document state, and permission
requirements, and the executed result is read back from the intended target.
