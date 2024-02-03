## use

use 是一个 React Hook，它可以让你读取类似于 Promise 或 context 的资源的值。

```js
const value = use(resource);
```

与其他 React Hook 不同的是，可以在循环和条件语句（如 `if`）中调用 `use`。但需要注意的是，调用 `use` 的函数仍然必须是一个组件或 Hook。

当使用 Promise 调用 `use` Hook 时，它会与 [`Suspense`](https://zh-hans.react.dev/reference/react/Suspense) 和 [错误边界](https://zh-hans.react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary) 集成。当传递给 `use` 的 Promise 处于 pending 时，调用 `use` 的组件也会 **挂起**。如果调用 `use` 的组件被包装在 Suspense 边界内，将显示后备 UI。一旦 Promise 被解决，Suspense 后备方案将被使用 `use` Hook 返回的数据替换。如果传递给 `use` 的 Promise 被拒绝，将显示最近错误边界的后备 UI。

### useCallback

`useCallback` 是一个允许你在多次渲染中缓存函数的 React Hook。

```js
const cachedFn = useCallback(fn, dependencies)
```

在组件顶层调用 `useCallback` 以便在多次渲染中缓存函数：

#### 参数

- `fn`：想要缓存的函数。此函数可以接受任何参数并且返回任何值。React 将会在初次渲染而非调用时返回该函数。当进行下一次渲染时，如果 `dependencies` 相比于上一次渲染时没有改变，那么 React 将会返回相同的函数。否则，React 将返回在最新一次渲染中传入的函数，并且将其缓存以便之后使用。React 不会调用此函数，而是返回此函数。你可以自己决定何时调用以及是否调用。

- `dependencies`：有关是否更新 `fn` 的所有响应式值的一个列表。响应式值包括 props、state，和所有在你组件内部直接声明的变量和函数。如果你的代码检查工具 [配置了 React](https://zh-hans.react.dev/learn/editor-setup#linting)，那么它将校验每一个正确指定为依赖的响应式值。依赖列表必须具有确切数量的项，并且必须像 `[dep1, dep2, dep3]` 这样编写。React 使用 [`Object.is`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is) 比较每一个依赖和它的之前的值。

#### 返回值

在初次渲染时，`useCallback` 返回你已经传入的 `fn` 函数

在之后的渲染中, 如果依赖没有改变，`useCallback` 返回上一次渲染中缓存的 `fn` 函数；否则返回这一次渲染传入的 `fn`。



### useContext

`useContext` 是一个 React Hook，可以让你读取和订阅组件中的 [context](https://zh-hans.react.dev/learn/passing-data-deeply-with-context)。

```js
const value = useContext(SomeContext)
```

#### 参数

- `SomeContext`：先前用 [`createContext`](https://zh-hans.react.dev/reference/react/createContext) 创建的 context。context 本身不包含信息，它只代表你可以提供或从组件中读取的信息类型。

#### 返回值

`useContext` 为调用组件返回 context 的值。它被确定为传递给树中调用组件上方最近的 `SomeContext.Provider` 的 `value`。如果没有这样的 provider，那么返回值将会是为创建该 context 传递给 [`createContext`](https://zh-hans.react.dev/reference/react/createContext) 的 `defaultValue`。返回的值始终是最新的。如果 context 发生变化，React 会自动重新渲染读取 context 的组件。

#### 用法

###### 向组件树深层传递数据

在组件的最顶级调用 `useContext` 来读取和订阅 [context](https://zh-hans.react.dev/learn/passing-data-deeply-with-context)。

```js
import { useContext } from 'react';

function Button() {
  const theme = useContext(ThemeContext);
  // ...
```

`useContext` 返回你向 context 传递的 context value。为了确定 context 值，React 搜索组件树，为这个特定的 context **向上查找最近的** context provider。

若要将 context 传递给 `Button`，请将其或其父组件之一包装到相应的 context provider：
