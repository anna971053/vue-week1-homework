<script setup>
import { ref } from 'vue';
const items = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20,
    isEdit: false //定義是否為編輯模式
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18,
    isEdit: false
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34,
    isEdit: false
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10,
    isEdit: false
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25,
    isEdit: false
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 25,
    isEdit: false
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18,
    isEdit: false
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20,
    isEdit: false
  },
])

const tempName = ref("");

const edit = {
  on: (item) => {
    // Method to enable edit mode for an item
    items.value.forEach(item => item.isEdit = false); // Disable edit mode for all items
    const index = items.value.findIndex(i => i.id === item.id); // Find the index of the item to be edited
    items.value[index].isEdit = true; // Enable edit mode for the selected item
    tempName.value = item.name; // Store the current name in tempName
  },
  // Method to save the edited name
  save: (item) => {
    item.name = tempName.value; // Update the item name with tempName value
    items.value.forEach(item => item.isEdit = false); // Disable edit mode for all items
  },
  // Method to cancel the edit operation
  cancle: (item) => {
    const index = items.value.findIndex(i => i.id === item.id); // Find the index of the item to be edited
    items.value[index].isEdit = false; // Disable edit mode for the selected item
  }
}

function addAmount(item) {
  item.stock++
}
function minusAmount(item) {
  if (item.stock > 0) {
    item.stock--
  }
}
</script>

<template>
  <div class="tx-note">雙擊品項名稱可修改該品項名稱</div>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in items" :key="item.id">
        <td @dblclick="edit.on(item)" class="editArea">
          {{ item.isEdit ? '' : item.name }}
          <div class="edit" v-if="item.isEdit">
            <input type="text" v-model="tempName">
            <button type="button" class="btn" @click="edit.save(item)">儲存</button>
            <button type="button" class="btn" @click="edit.cancle(item)">取消</button>
          </div>
        </td>
        <td>{{ item.description }}</td>
        <td>{{ item.price }}</td>
        <td><button class="btn" @:click="minusAmount(item)">-</button>{{ item.stock }}<button class="btn"
            @:click="addAmount(item)">+</button>
        </td>
      </tr>

    </tbody>
  </table>
</template>

<style scoped></style>
