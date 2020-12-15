<template>
  <div>
    <div v-for="(item, index) in filteredItem" :key="index">
      <list-item :item="item" class="item border-top my-auto p-2" v-on:itemchanged="$emit('reloadlist')" />
    </div>
  </div>
</template>

<script>
import listItem from "./listItem";
export default {
  props: ["filteredItem"],

  components: {
    listItem,
  },
};
</script>

<style>

</style>
