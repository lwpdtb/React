react.js 核心库 

react-dom.js 提供与 DOM 相关的功能

browser.min.js 将 JSX 语法转为 JavaScript 语法
***
  模板：ReactDOM.render() 


***
  组件（首字母大写）(virtual DOM)：React.createClass({})

  ***propTypes***        检测参数格式

 ***getDefaultProps***   设置默认值

 ***refs***            获取真实节点

> 1、作为一个特殊的属性，用过this.refs.获取

> 2、ref属性也可以是一个回调函数而不是一个名字。参照的组件作为函数的参数。

    render: function() {
    return (
      <TextInput
        ref={function(input) {
          if (input != null) {
            input.focus();
          }
        }} 
      />
    );
    },

 **当参照组件被卸载并且这个ref改变的时候，先前的ref的参数值将为null**

 ***getInitialState*** 只在组件被第一次渲染的时候被调用

  `React 提供一个工具方法 React.Children 来处理 this.props.children`

       this.setState() 
    
       this.state() 
    
       this.props()

       event.target.value()//textarea select radio

组件分为三个生命周期：

1. Mounting：已插入真实 DOM
1. Updating：正在被重新渲染
1. Unmounting：已移出真实 DOM


七种处理函数：

1. componentWillMount()
1. componentDidMount()
1. componentWillUpdate(object nextProps, object nextState)
1. componentDidUpdate(object prevProps, object prevState)
1. componentWillUnmount()
1. componentWillReceiveProps(object nextProps)：
1. shouldComponentUpdate(object nextProps, object nextState)：
   


***

# 创建React Component几种方式 #

### createClass ###

    var Greeting = React.createClass({});

### component ES6的类和继承 ###

    class Greeting extends React.Component {

         class Greeting extends React.Component {
         constructor(props) {//
         super(props);
         this.state = {count: props.initialCount};//（反模式）
         this.handleClick = this.handleClick.bind(this);
         }
    }
用这种方式创建组件时，React并没有对内部的函数，进行this绑定，所以如果你想让函数在回调中保持正确的this，就要手动对需要的函数进行this绑定。

### PureComponet ###

为了避免组件进行不必要的重新渲染，我们通过定义
> shouldComponentUpdate

来优化性能，通过判断props.color和state.count是否发生变化来决定需不需要重新渲染组件

    class CounterButton extends React.PureComponent {
    constructor(props) {
    super(props);
    this.state = {count: 1};
    }

### Stateless Functional Component ###

***

# 传递Props #
 **...other**

    var {checked , ...other} = this.props;//...other中是出了checked以外的所有的属性

 **…this.props**
   
> 比...other多了不管有没有明确使用，即包含所有属性

>     var player = {score: 1, name: 'Jeff'};
>     
>     var newPlayer = Object.assign({}, player, {score: 2});
>     //现在 player 没改变, 但是 newPlayer 是 {score: 2, name: 'Jeff'}
>     
>     // 或者如果你使用对象扩展语法，可以写成：
>     // var newPlayer = {...player, score: 2};


***

### 函数式组件 ###

只包含一个 render 方法。而不是通过扩展 **React.Component** 类定义的，函数式组件只需编写一个函数，传入 **props**(属性) 并返回应该渲染的内容就可以了

