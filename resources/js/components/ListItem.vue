<template>
    <div class="item">
        <h3><span class="item-title">{{item.id}} </span>{{item.task_name}}</h3>
        <p><span class="item-title">Исполнитель: </span>{{item.user_name}}</p>
        <p><span class="item-title">Описание: </span>{{item.task_description}}</p>
        <p><span class="item-title">Дата завершения: </span>{{item.task_completion_date}}</p>
        <span class="item-title">Статус: </span>
        <select>
            <option value="" selected disabled hidden>{{item.task_status}}</option>
            <!-- <option value="добавлена">добавлена</option> -->
            <option value="в работе">в работе</option>
            <option value="завершена">завершена</option>
        </select>
        <!-- <p><span class="item-title">Статус: </span>{{item.task_status}}</p> -->
        <p><span class="item-title">Дата создания: </span>{{item.created_at}}</p>
        <p><span class="item-title">Дата изменения: </span>{{item.updated_at}}</p>
    </div>
</template>

<script>
    export default {
        props: ['item']
    }
</script>

<style lang="scss" scoped>
.item-title {
    color: #a30000;
    font-weight: 600;
}
</style>