<script setup>
import { ref } from 'vue';

const text=ref('安德魯')
const num=ref(1);
const imgScr=ref('https://images.unsplash.com/photo-1719937206158-cad5e6775044?q=80&w=300&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D')
const add=()=>{
    num.value++
}
const todos=[
  {
    name:'購買雜貨',
    dueDate:'2024-07-30',
    complete:true
  },
  {
    name:'完成報告',
    dueDate:'2024-08-01',
    complete:false
  },
  {
    name:'清理房間',
    dueDate:'2024-09-30',
    complete:true
  },
  {
    name:'計劃假期',
    dueDate:'2024-07-30',
    complete:true
  },
  {
    name:'處理稅務',
    dueDate:'2024-06-28',
    complete:false
  },
]
</script>

<template>
    <h1>{{ text }}</h1>
    <input type="text" v-model="text">

    <h2>{{ num }}</h2>
    <button type="button" v-on:click="add">按我</button>
    <button type="button" @click="add">按我</button>

    <!-- 屬性 -->
     <img v-bind:src="imgScr" alt="">
     <img :src="imgScr" alt="">

     <div>
        <div v-for="todo in todos" v-bind:key="todo.id">
            {{ todo.name }}<br>
            {{ todo.dueDate }}<br>
            {{ todo.complete?'是':'否'}} <input type="checkbox" v-model="todo.complete">
            <hr>
        </div>
     </div>
</template>

<style scoped>
h1{
    font-weight: bold;
}
</style>