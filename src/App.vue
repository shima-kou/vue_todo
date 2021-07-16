<template>
  <div id="app">
    <ul class="mode_list">
      <li>
        <label for="allList"><input id="allList" type="radio" name="mode" v-model="mode" value="全て" />全て</label>
      </li>
      <li>
        <label for="workingList"><input id="workingList" type="radio" name="mode" v-model="mode" value="作業中" />作業中</label>
      </li>
      <li>
        <label for="completeList"><input id="completeList" type="radio" name="mode" v-model="mode" value="完了" />完了</label>
      </li>
    </ul>
    <TodoTable v-bind:todos="todos" v-bind:mode="mode" @deleteBtn="deleteRow" @statusBtn="changeStatus" />
    <TodoAdd v-bind:todos="todos" @addRow="row" />
  </div>
</template>

<script>
import TodoTable from './components/TodoTable.vue';
import TodoAdd from './components/TodoAdd.vue';

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      mode: '全て',
    };
  },
  methods: {
    row(value) {
      this.todos.push(value);
    },
    deleteRow(value) {
      const result = this.todos.findIndex((todo) => Number(todo.id) == Number(value));
      this.todos.splice(result, 1);
      for (let i = 0; i < this.todos.length; i++) {
        this.todos[i].id = Number(i + 1);
      }
    },
    changeStatus(value) {
      const result = this.todos.findIndex((todo) => Number(todo.id) == Number(value));
      if (this.todos[result]['status'] === '作業中') {
        this.todos[result]['status'] = '完了';
      } else {
        this.todos[result]['status'] = '作業中';
      }
    },
  },
  components: {
    TodoTable,
    TodoAdd,
  },
};
</script>

<style lang="scss">
@import './assets/css/main.css';
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
