<template>
    <div class="container">
        <div class="row align-items-center justify-content-center mx-0">
            <div class="col col-sm-8 col-md-7 col-lg-6 shadow p-1 pb-2">
                <div class="heading">
                    <h2 class="h2 pl-2 text-muted font-weight-bold" id="title">
                        Todo List
                    </h2>
                    <add-item-form v-on:reloadlist="getList()" />
                </div>

                <div class="">
                    <list-view
                        class="shadow"
                        :filter='filter'
                        :filteredItem='filteredItem()'
                        v-on:reloadlist="getList()"
                    />

                    <div class="my-3 mx-1">
                        <span class="text-muted"
                            ><span class="text-muted mx-1">
                                <a
                                    href="#"
                                    class="btn"
                                    :class="['shadow-sm', { selected: filter === 'all' }]"
                                    @click.prevent="filter = 'all'"
                                    >All tasks</a
                                >
                            </span></span
                        >
                        <span class="text-muted mx-2"
                            ><span class="text-muted mx-1">
                                <a
                                    href="#"
                                    class="btn"
                                    :class="['shadow-sm', { selected: filter === 'due' }]"
                                    @click.prevent="filter = 'due'"
                                    >Due</a
                                >
                            </span></span
                        >
                        <span class="text-muted"
                            ><span class="text-muted mx-1">
                                <a
                                    href="#"
                                    class="btn"
                                    :class="['shadow-sm', { selected: filter === 'done' }]"
                                    @click.prevent="filter = 'done'"
                                    >Completed</a
                                >
                            </span></span
                        >
                    </div>
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
        listView
    },

    data() {
        return {
            items: [],
            filter: 'all'
        };
    },
    methods: {
        getList() {
            axios
                .get("api/items")
                .then(response => {
                    this.items = response.data;
                })
                .catch(error => {
                    console.log(error);
                });
        },

        getItems() {
            return this.items.length;
        },

        due() {
            return this.items.filter(item => !item.completed).length;
        },

        completed() {
            return this.items.filter(item => item.completed).length;
        },
        filteredItem() {
            if (this.filter === "due") {
                return this.items.filter(item => !item.completed);
            } else if (this.filter === "done") {
                return this.items.filter(item => item.completed);
            }
            return this.items;
        }
    },
    created() {
        this.getList();
    }
};
</script>

<style scoped>
.heading {
    background: #fff;
    padding: 10px;
}
</style>
