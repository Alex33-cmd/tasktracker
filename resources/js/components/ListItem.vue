<template>
    <div :class="[selected == 'завершена' ? 'completed' : '', item]">
        <h3><span class="item-title">{{item.id}} </span>{{item.task_name}}</h3>
        <p><span class="item-title">Исполнитель: </span>{{item.user_name}}</p>
        <p><span class="item-title">Описание: </span>{{item.task_description}}</p>
        <p><span class="item-title">Дата завершения: </span>{{item.task_completion_date}}</p>

        <span class="item-title">Статус: </span>
        <select v-if="selected !== 'завершена'" @change="updateCheck()" v-model="selected">
            <option value="" selected disabled hidden>{{item.task_status}}</option>
            <!-- <option value="добавлена">добавлена</option> -->
            <option value="в работе">в работе</option>
            <option value="завершена">завершена</option>
        </select>
        <span v-else>завершена {{completionDate()}}</span>

        <!-- <p><span class="item-title">Статус: </span>{{item.task_status}}</p> -->
        <p><span class="item-title">Дата создания: </span>{{item.created_at}}</p>
        <p><span class="item-title">Дата изменения: </span>{{item.updated_at}}</p>
        <button @click="removeItem()" class="trashcan">Удалить</button>
    </div>
</template>

<script>
    export default {
        props: ['item'],

        data: function () {
                return {
                    selected: '',
                    date_completed: ''
                }
        },
        methods: {
            completionDate() {
                // Set completion date
                const date = new Date();
                const day = `${date.getDate()}`.padStart(2, 0);
                const month = `${date.getMonth() + 1}`.padStart(2, 0);
                const year = date.getFullYear();
                this.date_completed = `${year} ${month} ${day}`;
                return this.date_completed;
            },
            updateCheck() {
                if (this.selected == 'завершена') {

                    this.item.completed = true;
                    this.item.completed_at = this.date_completed;
                    this.item.task_status = 'завершена';

                    // PUT task status to DB
                    const apiUrlStore = 'api/item/' + this.item.id;

                    // put body data 
                    const bodyData = {
                        item: this.item
                    };

                    // request options
                    const optionsPUT = {
                        method: 'PUT',
                        body: JSON.stringify(bodyData),
                        headers: {
                            'Content-Type': 'application/json'
                        }
                    }

                    // send PUT request
                    fetch(apiUrlStore, optionsPUT)
                        .then(res => {
                            console.log('data successfuly saved');
                        })
                        .catch( error => {
                        console.log( error );
                    })
                }
            },

            removeItem() {
                
            }
        }
    }
</script>

<style lang="scss" scoped>
h3 {
    margin: 0;
}

select {
    box-sizing: border-box;
    background:#f7f7f7;
    border: none;
    outline: none;
    /* appearance: none; */
    z-index: 1;
    /* padding: 5px; */
    /* margin: 10px auto; */
    /* width: 50%; */
}
.item {
    box-sizing: border-box;
    display: block;
    background:#f7f7f7;
    position: relative;
    z-index: 1;
    padding: 15px;
    margin: 10px auto;
    width: 100%;
}
.completed {
    color: #999999;
    text-decoration: line-through;
}
.trashcan {
    padding: 10px;
}
.item-title {
    /* color: #a30000; */
    font-weight: 600;
}
</style>