<script setup>
import { ref } from "vue";

const datas = ref([
  {
    id: 1,
    name: "珍珠奶茶",
    description: "香濃奶茶搭配QQ珍珠",
    price: "50",
    stock: 20,
  },
  {
    id: 2,
    name: "冬瓜檸檬",
    description: "清新冬瓜配上新鮮檸檬",
    price: "45",
    stock: 18,
  },
  {
    id: 3,
    name: "翡翠檸檬",
    description: "綠茶與檸檬的完美結合",
    price: "55",
    stock: 34,
  },
  {
    id: 4,
    name: "四季春茶",
    description: "香醇四季春茶，回甘無比",
    price: "45",
    stock: 10,
  },
  {
    id: 5,
    name: "阿薩姆奶茶",
    description: "阿薩姆紅茶搭配香純鮮奶",
    price: "50",
    stock: 25,
  },
  {
    id: 6,
    name: "檸檬冰茶",
    description: "檸檬與冰茶的清新組合",
    price: "45",
    stock: 20,
  },
  {
    id: 7,
    name: "芒果綠茶",
    description: "芒果與綠茶的獨特風味",
    price: "55",
    stock: 18,
  },
  {
    id: 8,
    name: "抹茶拿鐵",
    description: "抹茶與鮮奶的絕配",
    price: "60",
    stock: 20,
  },
]);

// 定義一個函數來修改指定產品的庫存
const changStock = (id, stock) => {
  datas.value = datas.value.map((item) => {
    if (item.id === id) {
      item.stock = Math.max(stock, 0); // 確保庫存不低於 0
    }
    return item;
  });
};

// 定義一個函數來修改指定產品的名稱
const changeName = (id, newName) => {
  datas.value = datas.value.map((item) => {
    if (item.id === id) {
      item.name = newName; // 更新產品名稱
    }
    return item;
  });
};

// 定義一個可響應的物件，用來追踪每個產品是否處於編輯狀態
const editing = ref({});

// 定義一個函數來開始編輯指定產品的名稱
const startEditing = (id) => {
  editing.value[id] = true; // 設置產品的編輯狀態為 true
};

// 定義一個函數來保存指定產品的名稱並結束編輯狀態
const saveName = (id, newName) => {
  changeName(id, newName); // 更新產品名稱
  editing.value[id] = false; // 設置產品的編輯狀態為 false
};
</script>

<template>
  <h2>六角學院 2024 Vue 前端新手營week1</h2>
  <div class="table">
    <table>
      <thead>
        <tr>
          <th>品項</th>
          <th>描述</th>
          <th>價格</th>
          <th>庫存</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="data in datas" :key="data.id">
          <td>{{ data.name }}</td>
          <td><small>{{ data.description }}</small></td>
          <td>{{ data.price }}</td>
          <td>
            <button type="button" @click="changStock(data.id, data.stock - 1)">-</button>
            {{ data.stock }}
            <button type="button" @click="changStock(data.id, data.stock + 1)">+</button>
          </td>
          <td>
            <template v-if="editing[data.id]">
              <button @click="saveName(data.id, data.name)">保存</button>
              <input v-model="data.name" />
            </template>
            <template v-else>
              <button @click="startEditing(data.id)">修改</button>
            </template>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
