<template>
    <div class="todoList-container">
        <div class="todo-heading">
            <h2 class="title">Todo List</h2>
            <Form v-on:reloadlist="getList()" />
        </div>
        <div class="todo-content">
            <ListItem :items="items" v-on:reloadlist="getList()" />
        </div>
    </div>
</template>

<script>
import Form from "./addItem";
import ListItem from "./listView";

export default {
    name: "App",
    components: {
        Form,
        ListItem,
    },
    data() {
        return {
            items: [],
        };
    },
    methods: {
        getList() {
            axios
                .get("api/item")
                .then((res) => {
                    this.items = res.data;
                })
                .catch((err) => console.error(err));
        },
    },
    created() {
        this.getList();
    },
};
</script>
<style scoped>
.todoList-container {
    width: 400px;
    margin: auto;
}
.todo-heading {
    background: #f1dddd;
    padding: 10px;
}
.title {
    text-align: center;
}
</style>
