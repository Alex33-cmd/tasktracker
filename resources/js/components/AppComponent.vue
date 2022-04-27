<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Task Tracker App</h2>
            <add-item-form />
        </div>
        <list-view :itemProps="itemsFromDB" />
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
                itemsFromDB: []
            }
        },
        methods: {
            async getList() {

                const apiUrlGET = 'api/items';

                // request options
                const optionsGET = {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                }

                this.itemsFromDB = await (await fetch(apiUrlGET, optionsGET)).json()
                console.log(this.itemsFromDB);

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
        mounted() {
            this.getList()
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