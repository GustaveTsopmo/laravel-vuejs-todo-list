<template>
    <div class="item">
        <input
            class="checkbox "
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
        />

        <span :class="[item.completed ? 'completed' : '', 'item-text']">{{
            item.name
        }}</span>

        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props: ["item"],

    methods: {
        updateCheck() {
            axios
                .put("api/item/" + this.item.id, {
                    item: this.item
                })
                .then(response => {
                    if (response.status == 200) {
                        this.$dialog
                            .alert("Task updated successfully!")
                            .then(function(dialog) {
                                this.$emit("itemchanged");
                            });
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        },
        removeItem() {
            if(confirm('Do you really whant to delete this item?')){
                            axios
                .delete("api/item/" + this.item.id, {
                    item: this.item
                })
                .then(response => {
                    if (response.status == 200) {
                        return this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
            }
        }
    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: #999999;
}

.item-text {
    width: 100%;
    margin-left: 20px;
}

.checkbox {
    cursor: pointer;
}

.item {
    display: flex;
    justify-content: center;
    align-items: center;
}

.trashcan {
    background: transparent;
    border: none;
    color: #ff0000;
    outline: none;
    cursor: pointer;
}
</style>
