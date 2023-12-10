<script setup lang="ts">

import { ref } from 'vue'

var id = 2

interface Item {
  id: number
  name: string
  done: boolean
  important: boolean
}

const newItemName = ref('')
const newItemImportance = ref(false)

const items = ref<Item[]>([{ id: 0, name: "テストdone", done: true, important: false }, { id: 1, name: "テストundone", done: false, important: false }])

const addItem = () => {
  items.value.push({ id: id, name: newItemName.value, done: false, important: newItemImportance.value })
  newItemName.value = ''
  id++
}
const switchItem = (itemId: number) => {
  items.value[itemId].done = !items.value[itemId].done
}
</script>

<template>
  <h2>TodoList</h2>
  <h3>Tasks</h3>
  <ul v-for="item in items" :key="item.id" :class="{done: item.done,important:item.important&&!item.done}">
    <li>
      <div>
        {{ item.name }}
        <button @click="switchItem(item.id)" v-if="item.done">Return</button>
        <button @click="switchItem(item.id)" v-if="!item.done">Done!</button>
      </div>
    </li>
  </ul>

  <div>
    <label>
      <div>
        タスク名
        <input v-model="newItemName" type="text" />
      </div>
      <div>
        重要
        <input v-model="newItemImportance" type="checkbox" />
      </div>
    </label>
    <button @click="addItem">追加</button>

  </div>
</template>

<style>
.done {
  color: #aaaaaa;
}

.important {
  color: #aa2222;
  font-size: large;
}
</style>
