<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form />
        </div>
        <list-view />
    </div>
</template>

<script>
import addItemForm from "./AddItemForm.vue"
import listView from "./ListView.vue"

    export default {
        components: {
            addItemForm,
            listView
        }
    }
</script>

<style lang="scss" scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
    .heading {
        background: #e6e6e6;
        padding: 10px;
        #title {
            text-align: center;
            }
    }
}


</style>