<template>
    <div class="itemsListContainer">
        <div v-for="(itemProp, index) in itemProps" :key="index">
            <list-item
                :item="itemProp"
                class="item"
            />
        </div>
    </div>
</template>

<script>
import listItem from "./ListItem.vue"

    export default {
        props: ['itemProps'],
        components: {
            listItem
        }
    }
</script>

<style lang="scss" scoped>
.itemsListContainer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    .item {
        display: block;
        background:#f7f7f7;
        position: relative;
        z-index: 1;
        padding: 10px 0;
        margin: 10px auto;
        width: 100%;
    }
}

</style>