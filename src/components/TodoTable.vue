<template>
  <table id="todoTable">
    <thead>
      <tr>
        <th>ID</th>
        <th>コメント</th>
        <th>完了</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(todo, index) in filteredTodos(mode)" v-bind:key="index">
        <td>{{ todo.id }}</td>
        <td>{{ todo.text }}</td>
        <td>
          <button class="status_button" v-on:click="statusBtn(todo.id)" v-bind:status="todo.status">{{ todo.status }}</button>
        </td>
        <td><button class="delete_button" v-on:click="deleteBtn(todo.id)">削除</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'TodoTable',
  props: {
    todos: {
      type: Array,
      default: () => [],
    },
    mode: {
      type: String,
    },
  },
  computed: {},
  methods: {
    statusBtn(id) {
      this.$emit('statusBtn', id);
    },
    deleteBtn(id) {
      this.$emit('deleteBtn', id);
    },
    filteredTodos(status) {
      if (status === '作業中') {
        return this.todos.filter((todo) => todo.status === '作業中');
      }
      if (status === '完了') {
        return this.todos.filter((todo) => todo.status === '完了');
      }
      return this.todos;
    },
  },
};
</script>

<style scoped lang="scss"></style>
