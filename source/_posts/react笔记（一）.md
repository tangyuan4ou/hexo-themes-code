---
title: react笔记（一）
date: 2017-11-15 15:33:06
tags: ['react']
---

&nbsp;&nbsp;&nbsp;&nbsp;去年用react跟公司开发了一个项目，一直都是师傅带着我，项目是做好了，但是react这还是一直似懂非懂的，前段时间自己编写了一个hexo的主题，用react仿写了一下主题，没写完，但是还是决定抽时间总结一下。

## 组件化

&nbsp;&nbsp;&nbsp;&nbsp;提到react不得不提到组件化，组件化是react的特性之一，这也是也它风靡一时的原因之一。随着前端的发展，模块化，组件化已经成为一种趋势，它通过拆分dom使开发人员开发和维护网站更便利。

## 关于react


&nbsp;&nbsp;&nbsp;&nbsp;react是facebook开发的开源前端框架，主要针对view层、最近由于和苹果的问题，国内公司陆续中断了关于react的使用，但是我觉得react还是值得一学的，不论生命周期还是props、stste、refs。

&nbsp;&nbsp;&nbsp;&nbsp;写这个是为了回顾和总结一下最近学习的知识，笔记。

## 入门

&nbsp;&nbsp;&nbsp;&nbsp;提笔的时候发现入门有啥，尴尬😅，翻一翻[react中文](https://doc.react-china.org/)／[react英文](https://reactjs.org/)文档，天，这是什么，我就半年没有看竟然变成了这样，快速入门不再是当初的简单的几个数据的传递，变成了一个[游戏](https://codepen.io/gaearon/pen/gWWZgR?editors=0010),看来我确实荒废太久了。教程和文档写的非常详细，入门很适合看一下。

## 生命周期

&nbsp;&nbsp;&nbsp;&nbsp;React.Component是一个抽象基础类，因此直接引用React.Component几乎没有意义。相反，你通常会继承他，并且至少定义个一render()方法。

<div class="code">
<div class="codeHeight">
  Component()
</div>
`
class Greeting extends Component {
  render() {
    return <h1>Hello, Tangyuna</h1>;
  }
}
`
</div>

&nbsp;&nbsp;&nbsp;&nbsp;若你仍未使用 ES6，你可以使用 [create-react-class](https://doc.react-china.org/docs/react-without-es6.html)模块。

组件的生命周期分为几个阶段：

#### 装配
&nbsp;&nbsp;&nbsp;&nbsp;在组件实例被创建和插入DOM时被调用

> · constructor()  

&nbsp;&nbsp;&nbsp;&nbsp;组件的构造函数将会在装配之前调用

<div class="code">
<div class="codeHeight">
  constructor()
</div>
`
constructor(props) {
  super(props)
  this.state = {
    color: props.tangyuan
  }
  this.handleClick = this.handleClick.bind(this)
}
`
</div>

> · conponentWillMount() 

&nbsp;&nbsp;&nbsp;&nbsp;装配发生之前调用。也就是说在render之前调用，在这里设置状态是不会出发重渲的，避免在该方法中引入任何的副作用和订阅。

&nbsp;&nbsp;&nbsp;&nbsp;这是唯一会在服务端渲染调起的生命周期钩子函数，通常推荐使用constructor()

> · render() 

> · componentDidMount() 

&nbsp;&nbsp;&nbsp;&nbsp;在组建装配之后立即调用，初始化使DOM节点应该进行到这里，若需要从远端加载数据，这是一个很适合实现网络请求的地方，可设置状态出发重渲。

#### 更新
&nbsp;&nbsp;&nbsp;&nbsp;组件状态更新重新渲染，触发更新。调用一下方法。

> · componentWillReceiveProps(nextProps)

&nbsp;&nbsp;&nbsp;&nbsp;当组件传入props发生变化时调用，例如： 父组件状态改变，给予组件传入新的props值，用于组件peops变化后，更新state

> · shouldComponentUpdate()

&nbsp;&nbsp;&nbsp;&nbsp;我接触这个框架的时候react已经在中国大量下架了。所以我也没有深学所有的内容，这部分我也只是了解。

&nbsp;&nbsp;&nbsp;&nbsp;看过一些文章对这个方法的评价是，可提高性能，但是表现是微乎其微，并且隐藏bug会比较多，但是我并没有测试过。

&nbsp;&nbsp;&nbsp;&nbsp;编写这点需要使用不可变的状态，immutable.js或者Object.assign都可以。

> · componentWillUpdate(nextProps, nextState)

&nbsp;&nbsp;&nbsp;&nbsp;当props和state发生变化的时候执行，在render之前，初始化render的时候不执行，在这里不能使用this.props和this.state。

&nbsp;&nbsp;&nbsp;&nbsp;函数调用以后nextProps和nextState会被设置到this.props和this.state中，然后调用render方法更新洁面

> · render()

> · componentDidUpdate(prevProps, prevState)

&nbsp;&nbsp;&nbsp;&nbsp;组件更新结束之后执行，在初始化render时不执行

#### 卸载
&nbsp;&nbsp;&nbsp;&nbsp;当组件从DOM中移除的时候调用

> · componentWillUnmount()

&nbsp;&nbsp;&nbsp;&nbsp;当组件要被从界面上移除的时候，就会调用componentWillUnmount(),在这个函数中，可以做一些组件相关的清理工作，例如取消计时器、网络请求等。

### 其他api

> · setState()

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;设置state，属性值接受函数字符串和数值。

> · forceUpdate()

<div class="code">
<div class="codeHeight">
  forceUpdate()
</div>
`
this.state.valueWantChange = vale;
this.forceUpdate(); // this.setState(this.state);
`
</div>

&nbsp;&nbsp;&nbsp;&nbsp;在以下两种情况会用到 forceUpdate

&nbsp;&nbsp;&nbsp;&nbsp;· 手动更改了 state

&nbsp;&nbsp;&nbsp;&nbsp;·之后需要触发 render

&nbsp;&nbsp;&nbsp;&nbsp;做了除更改props和state之外的操作后，需要render。

&nbsp;&nbsp;&nbsp;&nbsp;但是使用forceUpdate 会跳过 shouldComponentUpdate 的过程，会触发子组件的所有lifeCycle方法（包括shouldComponentUpdate）从而造成性能的浪费。因此为了组件更加清晰高效，应该避免使用forceUpdate。

### 类属性

> · defaultProps

&nbsp;&nbsp;&nbsp;&nbsp;默认属性

<div class="code">
<div class="codeHeight">
  defaultProps
</div>
`
class Tangyuan extends React.Component {
  // ...
}

Tangyuan.defaultProps = {
  color: 'yellow'
};
`
</div>

> · displayName

&nbsp;&nbsp;&nbsp;&nbsp;displayName被用在调试信息中。JSX会自动设置该值

### 实例属性

> · props

> · state

## 总结

以上是我关于react生命周期的总结，既是总结也是笔记。方便日后翻阅，没有教学的功能。

后面会写一下关于props、state和ref的总结。





