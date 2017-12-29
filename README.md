# acorn-observable

## API Reference

### Cells

<a href="#cell_id" name="cell_id">#</a> <i>cell</i>.<b>id</b>

The name of the cell: null if the cell is anonymous; otherwise an Identifier or a ViewExpression. For example, a named expression cell:

```js
foo = 42
```

```json
{
  "type": "Identifier",
  "name": "foo"
}
```

Similarly, for a view expression cell:

```js
viewof foo = DOM.range()
```

```json
{
  "type": "ViewExpression",
  "id": {
    "type": "Identifier",
    "name": "foo"
  }
}
```

<a href="#cell_body" name="cell_body">#</a> <i>cell</i>.<b>body</b>

The body of the cell; null for an import or empty cell; otherwise a BlockStatement or an expression node. For example, a block cell:

```js
{
  return 42;
}
```

```json
{
  "type": "BlockStatement",
  "body": [
    {
      "type": "ReturnStatement",
      "argument": {
        "type": "Literal",
        "value": 42,
        "raw": "42"
      }
    }
  ]
}
```

Similarly, for an expression cell:

```js
42
```

```json
{
  "type": "Literal",
  "value": 42,
  "raw": "42"
}
```

<a href="#cell_async" name="cell_async">#</a> <i>cell</i>.<b>async</b>

Whether or not the cell body is asynchronous (*i.e.*, whether it contains an `await` statement). Always false for import and empty cells. For example, this expression cell is asynchronous:

```js
await new Promise(resolve => {
  setTimeout(() => {
    resolve(42)
  }, 250);
})
```

<a href="#cell_generator" name="cell_generator">#</a> <i>cell</i>.<b>generator</b>

Whether or not the cell body is a generator (*i.e.*, whether it contains a `yield` statement). Always false for import and empty cells. For example, this expression cell is a generator:

```js
yield* [1, 2, 3, 4]
```

### ViewExpression

<a href="#view_id" name="view_id">#</a> <i>view</i>.<b>id</b>

The view identifier: an Identifier.

### ImportSpecifier

<a href="specifier_view" name="specifier_view">#</a> <i>specifier</i>.<b>view</b>

True if the imported specifier is a view. For example:

```js
import {viewof foo} from "module"
```