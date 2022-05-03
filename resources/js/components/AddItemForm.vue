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
        <!-- <select v-model="itemData.task_status">
            <option value="" selected disabled hidden>Статус задачи</option>
            <option value="добавлена">добавлена</option>
            <option value="в работе">в работе</option>
            <option value="завершена">завершена</option>
        </select> -->
        <button @click="addItem()" :class="[ itemData.task_name ? 'active' : 'inactive', 'plus']"><b>+</b></button>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                itemData: {
                    task_name: "",
                    user_name: "",
                    task_description: "",
                    task_completion_date: "",
                    task_status: "добавлена"
                }
            }
        },
        methods: {
            addItem() {

                const apiUrlStore = 'api/item/store';

                // post body data 
                const bodyData = {
                    item: this.itemData
                };

                // request options
                const optionsPOST = {
                    method: 'POST',
                    body: JSON.stringify(bodyData),
                    headers: {
                        'Content-Type': 'application/json'
                    }
                }

                // send POST request
                fetch(apiUrlStore, optionsPOST)
                    .then(res => {
                        if( res.status == 201 ) {
                            // clearing fields
                            for (const prop of Object.getOwnPropertyNames(this.itemData)) {
                                this.itemData[prop] = '';
                            }
                            this.itemData.task_status = "добавлена";
                            this.$emit('reloadlist');
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
        box-sizing: border-box;
        display: block;
        background:#f7f7f7;
        border: none;
        outline: none;
        /* appearance: none; */
        position: relative;
        z-index: 1;
        padding: 10px;
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
        /* width: 100%; */
        width: 150px;
        /* height: 50px; */
        margin: 10px;
    }
    .active {
        color: #000000;
    }
    .inactive {
        color: #999999;
    }
}

</style>