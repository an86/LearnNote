# 1.reducer 的基本机构
    首先必须明确的是，整个应用只有一个单一的 reducer 函数：这个函数是传给 createStore 的第一个参数。一个单一的 reducer 最终需要做以下几件事：
    reducer 第一次被调用的时候，state 的值是 undefined。reducer 需要在 action 传入之前提供一个默认的 state 来处理这种情况。
    reducer 需要先前的 state 和 dispatch 的 action 来决定需要做什么事。
    假设需要更改数据，应该用更新后的数据创建新的对象或数组并返回它们。
    如果没有什么更改，应该返回当前存在的 state 本身。
# 2.state的基本结构。
    Redux 鼓励你根据要管理的数据来思考你的应用程序。数据就是你应用的 state，state 的结构和组织方式通常会称为 "shape"。在你组织 reducer 的逻辑时，state 的 shape 通常扮演一个重要的角色. 我们在构建reducer之前最好把应用的state整理出来。
{
  visibilityFilter: 'SHOW_ALL',
  todos: [
    {
      text: 'Consider using Redux',
      completed: true,
    },
    {
      text: 'Keep all state in a single tree',
      completed: false
    }
  ]
}
在这个例子中，todos 和 visibilityFilter 都是 state 的顶层 Key，他们分别代表着一个某个特定概念的数据切片。

大多数应用会处理多种数据类型，通常可以分为以下三类：
   a. 域数据（Domain data）: 应用需要展示、使用或者修改的数据（比如 从服务器检索到的所有 todos
   b. 应用状态（App state）: 特定于应用某个行为的数据（比如 “Todo #5 是现在选择的状态”，或者 “正在进行一个获取 Todos 的请求”）
   c. UI 状态（UI state）: 控制 UI 如何展示的数据（比如 “编写 TODO 模型的弹窗现在是展开的”）

一个典型的应用 state 大致会长这样：
{
    domainData1 : {},
    domainData2 : {},
    appState1 : {},
    appState2 : {},
    ui : {
        uiState1 : {},
        uiState2 : {},
    }
}

# 3.拆分reducer逻辑。
    拆分出来的新的函数通常分为3类。
    a. 一些小的工具函数，包含一些可重用的逻辑片段
    b.用于处理特定情况下的数据更新的函数，参数除了 (state, action) 之外，通常还包括其它参数
    c.处理给定 state 切片的所有更新的函数，参数格式通常为 (state, action)
# 4.reducer重构
    a.提取工具函数
    b.
        function updateObject(oldObject, newValues) {
            // 用空对象作为第一个参数传递给 Object.assign，以确保是复制数据，而不是去改变原来的数据
            return Object.assign({}, oldObject, newValues);
        }

        function updateItemInArray(array, itemId, updateItemCallback) {
            const updatedItems = array.map(item => {
                if(item.id !== itemId) {
                    // 因为我们只想更新一个项目，所以保留所有的其他项目
                    return item;
                }

                // 使用提供的回调来创建新的项目
                const updatedItem = updateItemCallback(item);
                return updatedItem;
            });
            return updatedItems;
        }
    c.提取case reducer
        function addTodo(state, action) {
            const newTodos = state.todos.concat({
                id: action.id,
                text: action.text,
                completed: false
            });
            return updateObject(state, {todos : newTodos});
        }
    d.按域拆分数据
    e.通过切片组合Reducer



#combineReducers 用法
不同 reducers 之间共享数据

#React中创建组件的方式
1.ES5写法：React.createClass

2.ES6写法：React.Component

3.无状态的函数写法，又称为纯组件SFC：无状态的函数创建的组件是无状态组件，它是一种只负责展示的纯组件著作权归作者所有。

const Todo = (props) => ( 
    <li 
        onClick={props.onClick} 
        style={{textDecoration: props.complete ? "line-through" : "none"}} 
    > 
        {props.text} 
    </li> 
)
对于props为 Object 类型时



