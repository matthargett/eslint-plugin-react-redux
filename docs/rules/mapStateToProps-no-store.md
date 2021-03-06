#  Enforces that mapStateToProps does not bind complete store to a component. (react-redux/mapStateToProps-no-store)

Passing whole state to a component is a bd practice. Triggering unnecessary re-renders.
Instead one should provide specific properties used by a component.

## Rule details

The following patterns are considered incorrect:

```js
const mapStateToProps = (state) => state
```

```js
const mapStateToProps = state => {
        return {state: state}
      }
```

```js
const mapStateToProps = state => ({...state});
```

```js
connect((state) => state, null)(App)
```

The following patterns are correct:

```js
const mapStateToProps = () => {}
```

```js
const mapStateToProps = (state) => {isActive: state.isActive}
```

```js
const mapStateToProps = ({isActive}) => {isActive}
```

```js
connect((state) => ({isActive: state.isActive}), null)(App)
```

## Not supported use cases.

Please note that the following use case although common is not supported due to the nature of static code analysis.

The following would not warn:

```js
const getProps = (state) => state;
const mapStateToProps = (state) => getProps(state);
```
