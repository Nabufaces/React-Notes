### 创建状态
```jsx harmony
    class Clock extends React.Component {
        constructor(props){
            super(props);
            this.state = {
                date: new Date()
            }
        }
        
        componentDidMount() {
            this.timeId = setInterval(() => {
                this.tick()
            }, 2000)
        }
        
        componentWillUnmount() {
            clearInterval(this.timeId)
        }
        
        tick(){
            this.setState({
                date: new Date()
            })
        }
        
        render(){
            return (
                <div>
                    <h1>{state.date.toLocaleDateString()}</h1>
                </div>
            )
        }
    }
    
    ReactDom.render(
        <Clock/>,
        document.getElementById('app')
    )
```

### 使用状态
#### 1. 不要直接更新状态，应当使用```setState()```:

```jsx harmony
    // Wrong
    this.state.comment = 'Hello';
    // Correct
    this.setState({comment: 'Hello'});
```
* 构造函数是唯一能够初始化```this.state```的地方。
        
#### 2. 状态更新可能是异步的
* React 可以将多个```setState()```调用合并成一个调用来提高性能。
* 因为```this.props```和```this.state```可能是异步更新的，你不应该依靠它们的值来计算下一个状态。

```jsx harmony
    // Wrong
    this.setState({
        counter: this.state.counter + this.props.increment
    })
    // Correct
    //该函数将接收先前的状态作为第一个参数，将此次更新被应用时的props做为第二个参数：
    this.setState((preState, props) => ({
        counter: preState.counter + props.increment
    }))
```

#### 3. 状态更新合并
* 当调用```setState()```修改组件状态时，只需要传入发生改变的State，而不是组件完整的State，因为组件State的更新是一个浅合并（Shallow Merge）的过程



### 数据自顶向下流动
* 子组件在其属性中接收到的参数，并不知道它是来自父组件的状态、还是来自父组件的属性、亦或手工输入。这通常被称为自顶向下或单向数据流。 任何状态始终由某些特定组件所有，并且从该状态导出的任何数据或 UI **只能影响树中下方的组件**。