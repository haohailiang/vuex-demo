# vuex-demo
vue状态管理插件使用

## vuex核心概念
### State
* 单一状态树
```javascript
const Counter = {
	template:`<div>{{count}}</div>`
	computed:{
		count(){
			return this.$store.state.count
		}
	}
}
```
### Getters
* 通过Getters可以派生出一些新的状态
```javascript
const store = new Vuex.Store({
	state:{
		todos:[
			{id:1, text:'...', done:true},
			{id:2, text:'...', done:false}
		]
	},
	getters:{
		doneTodos: state => {
			return state.todos.filter(todo => todo.done)
		}
	}
})
```
### Mutations
* 更改vuex的store中的状态的唯一方法是提交mulation
```javascript
const store = new Vuex.Store({
	state:{
		count:1
	},
	mutations:{
		increment(state){
			//变更状态
			state.count++
		}
	}
})
store.commit('increment')
```
### Actions
* Action提交的是mutation, 而不是直接变更状态
* Action可以包含任意异步操作
```javascript
const store = new Vuex.Store({
	state:{
		count:0
	},
	mutations:{//必须是同步的代码
		increment(state){
			//变更状态
			state.count++
		}
	},
	actions:{//可以是异步的代码
		increment(context){
			context.commit('increment')
		}
	}
})
```
### Modules
* 面对复杂的应用程序,当管理的状态比较多时,我们需要将vuex的store对象分割成模块(modules).
```javascript
const moduleA = {
	state:{ ... },
	mutations:{ ... },
	actions:{ ... },
	getters:{ ... }
}

const moduleB = {
	state:{ ... },
	mutations:{ ... },
	actions:{ ... }
}

const store = new Vuex.Store({
	modules:{
		a:moduleA,
		b:moduleB
	}
})
```




















