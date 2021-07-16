<template>
  <div class="ui_wrap">
    <h2>新規タスクの追加</h2>
    <div>
      <input id="comment_input" type="text" v-model="text" /><button id="addButton" v-on:click="addRow()">
        追加
      </button>
    </div>
    <transition name="fade">
      <p class="note" v-if="isShow === true && text === ''">テキストが入力されていません。</p>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'TodoAdd',
  data() {
    return {
      text: '',
      status: '作業中',
      isShow: false,
    };
  },
  props: {
    todos: {
      type: Array,
      default: () => [],
    },
  },
  watch: {},
  methods: {
    addRow() {
      if (this.text === '') {
        this.isShow = true;
        return;
      }
      const row = {
        id: this.$props.todos.length + 1,
        text: this.text,
        status: this.status,
      };
      this.text = '';
      this.isShow = false;
      this.$emit('addRow', row);
    },
  },
};
</script>

<style scoped lang="scss"></style>
