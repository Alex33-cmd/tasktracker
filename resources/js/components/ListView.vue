<template>
    <div>
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
.item {
    background: #e6e6e6;
    padding: 5px;
    margin-top: 5px;
    height: 50px;
}
</style>