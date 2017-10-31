### 基本用法
```jsx harmony
    function formatName(user) {
      return `${user.firstName} ${user.lastName}`
    }
    const user = {
        firstName: Nabufaces,
        lastName: Gao
    }
    const element = (
        <h1>
            Hello, {formatName(user)} !
        </h1>
    )
```

### JSX代表Objects
```jsx harmony
    const element = (
        <h1 className="greet">
            Hello World!
        </h1>
    )
```
等价于
```jsx harmony
    const element = React.createElement(
        'h1',
        {className: 'greet'},
        'Hello World!'
    )
```
等价于
```jsx harmony
    const element = {
        type: 'h1',
        props: {
            className: 'greet',
            children: 'Hello World!'
        }
    }
```