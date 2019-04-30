# cool-hooks

## use inputs
#### easy way to collect the data from many inputs at once without having to set up a state for all of them
```js
const useInputs = init => {
  const reducer = (state, { type, target, value }) => {
    switch (type) {
      case "modify":
        return { ...state, [target]: value };
      default:
        throw new Error(
          "There seems to be an error, are all your fields specified in init?"
        );
    }
  };

  const [state, dispatch] = useReducer(reducer, init);

  return [
    state,
    name => e =>
      dispatch({ type: "modify", target: name, value: e.target.value })
  ];
};
```
used like this: 
```js
const [state, onChange] = useInputs({
    //all input fields + their key
    name: "nm",
    age: "age",
    ...
  });
...
 <Input onChange={onChange("name")} value={state.name} />
```
