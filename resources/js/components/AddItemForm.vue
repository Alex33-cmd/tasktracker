<template>
    <div class="addItem">
        <input type="text" v-model="itemData.task_name" placeholder="Название задачи" />
        <!-- <input type="text" v-model="itemData.user_name" placeholder="Исполнитель" /> -->
        <select v-model="itemData.user_name">
            <option value="" selected disabled hidden>Исполнитель</option>
            <option value="Иванов А">Иванов А</option>
            <option value="Петров Б">Петров Б</option>
            <option value="Сидоров В">Сидоров В</option>
        </select>
        <input type="text" v-model="itemData.task_description" placeholder="Описание задачи" />
        <input type="date" v-model="itemData.task_completion_date" :class="[ itemData.task_completion_date ? 'active' : 'inactive']" />
        <select v-model="itemData.task_status">
            <option value="" selected disabled hidden>Статус задачи</option>
            <option value="добавлена">добавлена</option>
            <option value="в работе">в работе</option>
            <option value="завершена">завершена</option>
        </select>
        <button @click="addItem()" :class="[ itemData.task_name ? 'active' : 'inactive', 'plus']"><b>+</b></button>
    </div>
</template>

<script>
// import axios from "axios";
// import { response } from "express";

    export default {
        data: function () {
            return {
                itemData: {
                    task_name: "",
                    user_name: "",
                    task_description: "",
                    task_completion_date: "",
                    task_status: ""
                }
            }
        },
        methods: {
            addItem() {
                // if( this.item.name == '' ) {
                //     return;
                // }
                
                // axios.post('api/item/store', {
                //     item: this.item
                // })
                // .then( response => {
                //     if( response.status == 201 ) {
                //         this.item.name = '';
                //     }
                // })
                // .catch( error => {
                //     console.log( error );
                // })

                const apiUrl = 'api/item/store';

                // post body data 
                const bodyData = {
                    item: this.itemData
                };

                // request options
                const options = {
                    method: 'POST',
                    body: JSON.stringify(bodyData),
                    headers: {
                        'Content-Type': 'application/json'
                    }
                }

                // send POST request
                fetch(apiUrl, options)
                    .then(res => {
                        if( res.status == 201 ) {
                            // clearing fields
                            for (const prop of Object.getOwnPropertyNames(this.itemData)) {
                                this.itemData[prop] = '';
                            }
                        }
                    })
                    .catch( error => {
                    console.log( error );
                })
            }
        }
    }
</script>

<style lang="scss" scoped>
.addItem {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    input, select {
        display: block;
        background:#f7f7f7;
        border: none;
        outline: none;
        appearance: none;
        position: relative;
        z-index: 1;
        outline: none;
        padding: 10px 0;
        margin: 10px auto;
        width: 100%;
    }

    select:invalid {
        color: #999999;
    }
    select option[value=""] {
        color: #999999;
    }

    .plus {
        font-size: 30px;
        width: 100%;
        /* width: 50px; */
        height: 50px;
    }
    .active {
        color: #000000;
    }
    .inactive {
        color: #999999;
    }
}

</style>