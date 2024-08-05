<script setup>
import {ref} from "vue"; //定義vue的資料使用
const text=ref('一句話')
// 雙向綁定

// 把資料抽出來
// 由資料驅動畫面
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
<h1>代辦清單練習</h1>
<h2>{{ text }}</h2>
<input type="text" v-model="text" >
 <table>
  <thead>
    <tr>
      <th>代辦事項名稱</th>
      <th>到期日</th>
      <th>是否已完成</th>
    </tr>
  </thead>
  <tbody>
    <!-- forEach -->
    <tr v-for="todo in todos" :key="todo.id">
      <td>{{ todo.name }}</td>
      <td>{{ todo.dueDate }}</td>
      <td>{{ todo.complete?'是': '否'}}</td>
      <!-- 三元運算式 -->
    </tr>
    
  </tbody>
</table>

</template>

<style>
h1,th{
  font-weight: bold;
}
</style>