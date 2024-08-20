<script setup>
import { ref } from 'vue';
const data=[
  {
    id:1,
    name:'香濃奶茶搭配QQ珍珠',
    describe:'香濃奶茶搭配QQ珍珠',
    price:50,
    stock:20,
  },
  {
    id:2,
    name:'冬瓜檸檬',
    describe:'清新冬瓜配上新鮮檸檬珠',
    price:45,
    stock:18,
  },
  {
    id:3,
    name:'翡翠檸檬',
    describe:'綠茶與檸檬的完美結合',
    price:55,
    stock:34,
  },
  {
    id:4,
    name:'四季春茶',
    describe:'香醇四季春茶，回甘無比',
    price:45,
    stock:1,
  },
  {
    id:5,
    name:'阿薩姆奶茶',
    describe:'阿薩姆紅茶搭配香醇鮮奶珠',
    price:50,
    stock:25,
  },
  {
    id:6,
    name:'檸檬冰茶',
    describe:'檸檬與冰茶的清新組合',
    price:50,
    stock:7,
  },
  {
    id:7,
    name:'芒果綠茶',
    describe:'芒果與綠茶的獨特風味',
    price:100,
    stock:2,
  },
  {
    id:8,
    name:'芒抹茶拿鐵',
    describe:'抹茶與鮮奶的絕配',
    price:50,
    stock:3,
  },

]


const drinks = ref(data);

// 庫存增減
function changeStockNum(id, stock) {
  drinks.value = drinks.value.map((item) => {
    if (item.id === id) {
      item.stock = stock;
    }
    return item;
  });
}

const tempEdite=ref({
  id:'',
  text:''
})

const changeEdit=(item)=>{
 tempEdite.value={...item}; //拷貝
 console.log(tempEdite.value);
//  傳參考概念
}

const comfirmEdit=()=>{
  const index=drinks.value.findIndex(item=>item.id===tempEdite.value.id)
  console.log(tempEdite.value);
  // 把值覆蓋回去,針對索引位置-index覆蓋
  drinks.value[index]=tempEdite.value;
  
  // 編輯區域框框還原
  tempEdite.value={}
}

</script>

<template>
<link href='https://fonts.googleapis.com/css?family=Noto Sans TC' rel='stylesheet'>
  <div class="container">
    <h1>Vue點餐機</h1>
    <h3>六角學院 2024 Vue 前端新手營 by Andrew</h3>


    <table class="content table-hover">
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col">操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in drinks" :key="item.id">
          <td class="name">{{ item.name }}</td>
          <td class="describe">{{ item.describe }}</td>
          <td>{{ item.price }}</td>
          <td class="stock">
            <button @click="changeStockNum(item.id, item.stock - 1)" :disabled="item.stock < 1">-</button>
            {{ item.stock }}
            <button @click="changeStockNum(item.id, item.stock + 1)">+</button>
          </td>
          <td class="edit">
            <button @click="changeEdit(item)">編輯</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="tempEdite.id" class="edit-area">
      <h2>編輯區域</h2>
      <label>
        當前修改的區域: {{ tempEdite.name }}
        <input type="text" v-model="tempEdite.name" />
      </label>
      <button @click="comfirmEdit">確認編輯</button>
      <button @click="tempEdite = {}">取消編輯</button>
    </div>
  </div>
</template>

<style scoped>


body {
  margin: 0;
  padding: 0;
  background-color: #ffffff !important; /* 設置整個網頁背景為白色 */
  color: black;
  font-family: 'Noto Sans TC', sans-serif; /* 確保使用正確的字體 */
  /* 默認情況下也使 body 內容居中 */
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}


th{
  color: #ffffff;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center; /* 垂直置中 */
  align-items: center; /* 水平置中 */
  min-height: 100vh; /* 確保容器高度至少為視窗高度 */
}

h1, h2, h3 {
  text-align: center;
  font-weight: 700;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

.table-hover > tbody > tr:hover > * {
	background-color: rgb(91, 91, 91);
  color: #ffffff;
}

th, td {
  border: 1px solid #bababa;
  padding: 10px;
  text-align: center;
}

.name,.stock{
  width: 150px; /* 調整這裡的寬度以適應你的需求 */
}
.describe {
  width: 300px;
}

th {
  background-color: #353535;
  margin-top: 30px;
}

button {
  margin: 0 5px;
}

.edit-area {
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #505050;
  background-color: #f9f9f9;
}

label {
  display: block;
  margin-bottom: 10px;
}
</style> 
