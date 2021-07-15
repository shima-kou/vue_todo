<template>
  <div id="app">
    <ul class="status_list">
      <li>
        <label for="allList"><input id="allList" type="radio" name="mode" v-model="mode" value="全て" />全て</label>
      </li>
      <li>
        <label for="nowList"><input id="nowList" type="radio" name="mode" v-model="mode" value="作業中" />作業中</label>
      </li>
      <li>
        <label for="complete"><input id="complete" type="radio" name="mode" v-model="mode" value="完了" />完了</label>
      </li>
    </ul>
    <TodoTable v-bind:list="tableList" v-bind:mode="mode" @deleteBtn="deleteRow" @statusBtn="changeStatus" />
    <TodoAdd v-bind:list="tableList" @addRow="row" />
  </div>
</template>

<script>
import TodoTable from './components/TodoTable.vue';
import TodoAdd from './components/TodoAdd.vue';

export default {
  name: 'App',
  data() {
    return {
      tableList: [],
      mode: '全て',
    };
  },
  methods: {
    row(value) {
      this.tableList.push(value);
    },
    deleteRow(value) {
      const result = this.tableList.findIndex((t) => Number(t.id) == Number(value));
      this.tableList.splice(result, 1);
      for (let i = 0; i < this.tableList.length; i++) {
        this.tableList[i].id = Number(i + 1);
      }
    },
    changeStatus(value) {
      const result = this.tableList.findIndex((t) => Number(t.id) == Number(value));
      if (this.tableList[result]['status'] === '作業中') {
        this.tableList[result]['status'] = '完了';
      } else {
        this.tableList[result]['status'] = '作業中';
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
