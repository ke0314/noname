<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'
export default{
  data(){
    return {
      todoItems:[]/*데이터 속성 선언*/
    }

  },

  created(){/*컴포넌트 생성시실행 */
    if (localStorage.length > 0){
      for (var i =0; i < localStorage.length; i++){
        this.todoItems.push(localStorage.key(i))
      }
    }
  },
  methods:{
    addTodo(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem)
    },
    clearAll(){
      localStorage.clear();
      this.todoItems=[];
    },
    removeTodo(todoItem, index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1); /* splice(index,1) 배열의 특정 index에서 부여한 숫자만큼의 인덱스를 삭제 */
    }
  },
  
  components:{
    'TodoHeader' :TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>


<style>
body{
  text-align: center;
  background-color: #F6F6F8;
}
input{
    border-style: groove;
    width:200px;
}
button{
    border-style: groove;
}
.shadow{
    box-shadow: 5px 10px 10px rbga(0,0,0,0.03);
}
</style>