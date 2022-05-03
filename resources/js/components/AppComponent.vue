<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 class="title">Task Tracker App</h2>
            <add-item-form
            v-on:reloadlist="getList()" />
        </div>
        <div class="heading">
            <h2 class="title">Task Tracker App</h2>
            <span>Сортировка: </span>
            <select @change="getList()" v-model="taskFilter">
                <option value="user_name">Исполнитель</option>
                <option value="task_status">Статус</option>
                <option value="task_completion_date">Дата завершения</option>
                <option value="completed_at">Дата выполнения</option>
                <option value="created_at">Дата создания</option>
            </select>
            <list-view 
                :itemProps="itemsFromDB"
                v-on:reloadlist="getList()" />
        </div>
        
    </div>
</template>

<script>
import addItemForm from "./AddItemForm.vue"
import listView from "./ListView.vue"

    export default {
        components: {
            addItemForm,
            listView
        },
        data: function () {
            return {
                itemsFromDB: [],
                taskFilter: 'created_at'
            }
        },
        methods: {
            async getList() {

                const apiUrlGET = 'api/items/' + this.taskFilter;

                // request options
                const optionsGET = {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                }

                this.itemsFromDB = await (await fetch(apiUrlGET, optionsGET)).json()

                // send GET request
                // fetch(apiUrlGET, optionsGET)
                //     .then(res => {
                //         // this.itemsFromDB = res
                //         console.log(res.json());
                //     })
                //     .catch( error => {
                //     console.log( error );
                // })
            },
        },
        created() {
            this.getList()
        }
    }
</script>

<style lang="scss" scoped>
.todoListContainer {
    background: #000;
    display: grid;
    /* grid-template-columns: repeat(2, 1fr); */
    grid-template-columns: 1fr 2fr;
    /* gap: 10px; */
    width: 100%;
    /* margin: auto; */
    .heading {
        background: #e6e6e6;
        padding: 20px;
        margin: 20px;
        .title {
            text-align: center;
        }
    }
}


</style>