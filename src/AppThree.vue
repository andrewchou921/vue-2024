<script setup>
import { ref } from 'vue';

const text=ref('這是一段文字')

const addTodo=()=>{
    todos.value.push({
        text:text.value,
        id: new Date().getTime()
    })
}

const todos=ref([
    {
      id:123,
      text:'12345',
      imageUrl:
      'https://images.unsplash.com/photo-1719937206158-cad5e6775044?q=80&w=300&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
   }
])

const tempEdite=ref({
  id:'',
  text:'',
})

const deleteTodo=(todo)=>{
   console.log(todo);
   const index=todos.value.findIndex(item=>item.id===todo.id)
  //  js陣列方法 卡斯柏老師有在yt放教學影片
   console.log(index);
   
   todos.value.splice(index,1)
}

const prepareEdit=(todo)=>{
 tempEdite.value={...todo}; //拷貝
 console.log(tempEdite.value);
//  傳參考概念
}

const comfirmEdit=()=>{
  const index=todos.value.findIndex(item=>item.id===tempEdite.value.id)
  console.log(tempEdite.value);
  // 把值覆蓋回去,針對索引位置-index覆蓋
  todos.value[index]=tempEdite.value;
  // 編輯區域框框還原
  tempEdite.value={}
}
</script>

<template>
  <input type="text" v-model="text">
  <button type="button" @click="addTodo">新增</button>

  <div v-for="todo in todos" :key="todo.id">
    {{ todo.text }} 
    <button type="button" @click="deleteTodo(todo)">刪除</button>
    <button type="button" @click="prepareEdit(todo)">編輯</button>
    <img :src="todo.imageUrl" alt="">
    <hr>
  </div>

 <hr>
 <div v-if="tempEdite.id">
  <h2>編輯區域</h2>
  當前修改的值:{{tempEdite.text}} <br>
  <input type="text" v-model="tempEdite.text">
  <button type="button" @click="comfirmEdit">確認編輯</button>
  <button type="button" @click="tempEdite={}">取消編輯</button>
 </div>

</template>

<style>
</style>