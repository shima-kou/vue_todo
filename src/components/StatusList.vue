<template>
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
</template>

<script>
export default {
  name: 'StatusList',
  props: {
    mode: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
