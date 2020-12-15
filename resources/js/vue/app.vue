<template>
  <div class="container ">
    <div class="row align-items-center justify-content-center mx-0">
      <div class="col col-sm-8 col-md-7 col-lg-6 shadow p-1 pb-2">
        <div class="heading">
          <h2 class="h2 pl-2 text-muted font-weight-bold" id="title">Todo List</h2>
          <add-item-form v-on:reloadlist="getList()" />
        </div>

        <div class="shadow">
          <list-view class="shadow" :items="items" v-on:reloadlist="getList()" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import addItemForm from "./addItemForm";
import listView from "./listView";

export default {
  components: {
    addItemForm,
    listView,
  },

  data() {
    return {
      items: [],
    };
  },
  methods: {
    getList() {
      axios
        .get("api/items")
        .then((response) => {
          this.items = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },

  created() {
    this.getList();
  },
};
</script>

<style scoped>
.heading {
  background: #fff;
  padding: 10px;
}
</style>
