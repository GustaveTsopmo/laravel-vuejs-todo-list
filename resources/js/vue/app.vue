<template>
  <div class="todo-list-container bg-dark">
    <div class="heading">
      <h2 class="h2" id="title">Todo List</h2>
      <add-item-form v-on:reloadlist="getList()" />
    </div>

    <list-view :items="items" v-on:reloadlist="getList()" />
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
  }
};
</script>

<style scoped>
.todo-list-container {
  width: 350px;
  margin: auto;
}

.heading {
  background: #e6e6e6;
  padding: 10px;
}

#title {
  text-align: center;
}
</style>
