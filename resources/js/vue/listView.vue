<template>
  <div>
    <div v-for="(item, index) in items" :key="index">
      <list-item :item="item" class="item border-top my-auto p-2" v-on:itemchanged="$emit('reloadlist')" />
    </div>
  </div>
</template>

<script>
import listItem from "./listItem";
export default {
  props: ["items"],

  components: {
    listItem,
  },
};
</script>

<style>

</style>
