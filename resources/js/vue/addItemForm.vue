<template>
  <div class="row justify-content-center">
    <div class="input-group">
      <input
        type="text"
        v-model="item.name"
        class="form-control border-top-0 border-start-0 border-right-0 rounded-0 bg-transparent shadow-sm"
        placeholder="New task name..."
        aria-describedby="button-addon2"
      />
      <button
        @click="addItem()"
        :class="[item.name ? 'btn-success' : 'btn-outline-light text-muted', 'shadow-none y-auto']"
        id="button-addon2"
      >
      <i :class="[item.name ? 'fas fa-plus-square' : 'fas fa-plus-square disabled']"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      item: {
        name: "",
      },
    };
  },
  methods: {
    addItem() {
      if (this.item.name === "") {
        return;
      }
      axios
        .post("api/item/store", {
          item: this.item,
        })
        .then((response) => {
          if (response.status === 201) {
            this.item.name = "";
            this.$emit("reloadlist");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
.add-item {
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
