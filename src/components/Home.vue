<template>
  <div class="hello">
    <auto v-model="value" label="Nome do produto" :items="[{name: 'Vicfff', age: 20}, {name: 'Vicffffgg', age: 20}, {name: 'Vicfff', age: 20}, {name: 'Vicfff', age: 20}, {name: 'Vicfff', age: 20}, {name: 'Vicfff', age: 20},{name: 'Vicfff', age: 20},{name: 'Vicfff', age: 20},{name: 'Vicfff', age: 20},{name: 'Vicfff', age: 20},{name: 'Vicfff', age: 20},{name: 'Vicfff', age: 20}]"></auto>
  </div>
</template>

<script>
import auto from "./Autocomplete.vue";
export default {
  name: "HelloWorld",
  data() {
    return {
      value: ""
    };
  },
  props: {
    msg: String
  },
  components: {
    auto
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
h3
  margin 40px 0 0

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
