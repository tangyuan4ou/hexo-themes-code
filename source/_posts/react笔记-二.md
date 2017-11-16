---
title: react笔记（二）
date: 2017-11-16 10:14:51
tags: 'react'
---

&nbsp;&nbsp;&nbsp;&nbsp;这部分是关于react props，state和ref的整理

props和state都可以用来传递数据：

### props
&nbsp;&nbsp;&nbsp;&nbsp;props只读性，官方说法是：无论是使用函数或者类来声明一个组件，它绝对不能修改它自己的props。

<div class="code">
<div class="codeHeight">
  props传参方式：
</div>
`
class Tangyuan extends React.Component {
    render() {
        return (
            <div>hello, {this.props.name}</div>
        )
    }
}

class Youyou extends React.Component {
    render() {
        return (
            <Tangyuan name="tangyuan" />
        )
    }
}

ReactDOM.render(
  <Youyou />,
  document.getElementById('root')
);
`
</div>

### state

&nbsp;&nbsp;&nbsp;&nbsp;state可以根据交互来改变，这就是为什么有一些容器组件需要定义state来更新和修改数据，而子组件只能通过props来传递数据。

<div class="code">
<div class="codeHeight">
    state
</div>
`
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}

class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <FormattedDate date={this.state.date} />
      </div>
    );
  }
}

function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
`
</div>

### refs

refs的使用情况：

> · 处理焦点、文本选择或媒体控制。

> · 触发强制动画

> · 集成第三方DOM库

&nbsp;&nbsp;&nbsp;&nbsp;如果可以通过声明实现，则尽量避免使用refs

##### 不要过度使用refs

&nbsp;&nbsp;&nbsp;&nbsp;多在组件中使用state，因为较高级别的state更清晰。

添加方式：

<div class="code">
<div class="codeHeight">
  refs
</div>
`
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.focus = this.focus.bind(this);
  }

  focus() {
    // 直接使用原生 API 使 text 输入框获得焦点
    this.textInput.focus();
  }

  render() {
    // 使用 'ref' 的回调将 text 输入框的 DOM 节点存储到 React 
    // 实例上（比如 this.textInput）
    return (
      <div>
        <input
          type="text"
          ref={(input) => { this.textInput = input; }} />

        <input
          type="button"
          value="Focus the text input"
          onClick={this.focus}
        />
      </div>
    );
  }
}
`
</div>

还有可以：

<div class="code">
<div class="codeHeight">
    refs
</div>
`
this.refs.yourRefname.你的操作   //获取
<div ref="yourRefname"></div>  //设置
`
</div>

&nbsp;&nbsp;&nbsp;&nbsp;以上就是我对react的我常用且容易混淆的知识点的总结。

