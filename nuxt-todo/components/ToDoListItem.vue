<template>
  <div class="to-do-item" :class="{ completed: todo.completed }">
    <span>{{ todo.todoTitle }}</span>
    <div class="controls">
      <span @click="deleteItem(todo)">❌</span>
      <span @click="completeItem(todo)">✅</span>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  props: {
    todo: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  methods: {
    async completeItem(todo) {
      if (todo.completed) {
        await axios.put('http://localhost:1337/todos/' + todo.id, {
          completed: false,
        })
      } else {
        await axios.put('http://localhost:1337/todos/' + todo.id, {
          completed: true,
        })
      }
      this.$router.go()
    },
    async deleteItem(todo) {
      await axios.delete('http://localhost:1337/todos/' + todo.id)
      this.$router.go()
    },
  },
}
</script>

<style>
.to-do-item {
  width: 100%;
  display: block;
  height: 50px;
  border-top: solid 1px #eeeeee;
  font-size: 24px;
}
.completed {
  opacity: 0.4;
}
.to-do-item span {
  height: 50px;
  padding-left: 20px;
  line-height: 50px;
  width: 450px;
  text-align: left;
  display: inline-block;
}
.to-do-item .controls {
  display: inline-block;
  height: 50px;
  line-height: 50px;
  float: right;
}
.to-do-item .controls span {
  line-height: 50px;
  height: 50px;
  display: inline-block;
  width: 45px;
  text-align: center;
  padding: 0;
  cursor: pointer;
}
</style>
