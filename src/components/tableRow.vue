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
    <tbody v-if="mode === '全て'">
      <tr v-for="(tr, n) in list" v-bind:key="n">
        <td>{{ tr.id }}</td>
        <td>{{ tr.text }}</td>
        <td>
          <button class="status_button" v-on:click="statusBtn" v-bind:data-id="tr.id" v-bind:status="tr.status">{{ tr.status }}</button>
        </td>
        <td><button class="delete_button" v-on:click="deleteBtn" v-bind:data-id="tr.id">削除</button></td>
      </tr>
    </tbody>
    <tbody v-if="mode === '作業中'">
      <tr v-for="(tr, n) in filteredWorking" v-bind:key="n">
        <td>{{ tr.id }}</td>
        <td>{{ tr.text }}</td>
        <td>
          <button class="status_button" v-on:click="statusBtn" v-bind:data-id="tr.id" v-bind:status="tr.status">{{ tr.status }}</button>
        </td>
        <td><button class="delete_button" v-on:click="deleteBtn" v-bind:data-id="tr.id">削除</button></td>
      </tr>
    </tbody>
    <tbody v-if="mode === '完了'">
      <tr v-for="(tr, n) in filteredComplete" v-bind:key="n">
        <td>{{ tr.id }}</td>
        <td>{{ tr.text }}</td>
        <td>
          <button class="status_button" v-on:click="statusBtn" v-bind:data-id="tr.id" v-bind:status="tr.status">{{ tr.status }}</button>
        </td>
        <td><button class="delete_button" v-on:click="deleteBtn" v-bind:data-id="tr.id">削除</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'TodoTable',
  props: {
    list: {
      type: Array,
      default: () => [],
    },
    mode: {
      type: String,
    },
  },
  computed: {
    filteredWorking() {
      return this.list.filter((li) => li.status === '作業中');
    },
    filteredComplete() {
      return this.list.filter((li) => li.status === '完了');
    },
  },
  methods: {
    statusBtn(event) {
      this.$emit('statusBtn', event.currentTarget.getAttribute('data-id'));
    },
    deleteBtn(event) {
      this.$emit('deleteBtn', event.currentTarget.getAttribute('data-id'));
    },
  },
};
</script>

<style scoped lang="scss"></style>
