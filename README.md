# dva_from0_guide
从零开始的DVA教程(1)
# 前言
React的框架千变万化,从React-Redux到ReactRouter等等,都方便了React的开发, DVA与UMI便是其中之一.  
DVA是蚂蚁金服体验技术部看到了市场上redux, saga等大量技术的产生而导致的各种问题,不方便而将这些东西全部打包成的一个新的框架.  
不,没有新的东西,DVA并没有创建任何新的概念,它只是将这些东西全都揉到了一块去,用更简便的方式调用.  
如果你学过redux,换用DVA会很简单,因为许多语法都是共通的,包括connect, mapStateToProps, dispatch等等. 你只需要把格式换成DVA的格式就可以尽情享用DVA框架带来的便利.  
如果你没学过redux,我个人建议你学习一下概念,但你如果坚持继续看下去,我也会倾尽全力的把流程讲清楚, 用各种各样的例子.  
下面这张图你们应该在[DVA概念](https://dvajs.com/guide/concepts.html)里见过:  
![DVA](https://zos.alipayobjects.com/rmsportal/PPrerEAKbIoDZYr.png)  
我不知道有多少人是不是和我一样第一眼看到的时候只感觉云里雾里,弯来绕去的,反正我是这个感觉, 因为没看懂.  
让我们来用我们自己这具身体来举个例子吧,等例子看完,我觉得你就明白了.  

# 例子
## Action
让我们先从外部事件开始吧. 一个用户的点击,输入,都是一个外部事件,在例子中,我们假设你被要求说出一个'我'字来.  
我们收到了这个请求,然后我们的大脑决定照着这个做, 那么我们的大脑就创建了一个**Action(行为)**. Action是一个对象,在这个例子里,我们假设这个对象是:
```javascript
{
  type:'mouth/speak',
  payload:{
    words:'我'
  }
}
```
这就是一个完整的action对象,对象里有一个type属性描述了这个action要做什么,payload是参数,完成这个action所需要的参数,在这里是一个"我"字作为参数.  
type属性是约定属性,每个action里都得有个type属性在第一层.  

但这action只是个普通的对象, 如果要把它付诸行动, 那么我们就要把这个action进入到执行阶段.  
## Model.dispatch
大脑完成action之后,需要将这个action下发下去, 发给谁呢? 大脑的神经网络(DVA)在收到这个action之后,会先查看type(类似收件人地址), 根据type去寻找action的接收人,在例子中是mouth/speak, 也就是说会将这个action发给mouth这个部位下面的speak这个dispatch.  
dispatch是一个function(函数), 只是一个函数,没有什么复杂的东西,它的作用就是接收参数,然后根据参数修改state. 
