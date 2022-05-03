<template>
    <div class="itemsListContainer">
        <div v-for="(itemProp, index) in itemProps" :key="index">
            <list-item
                :item="itemProp"
                class="item"
                v-on:itemchanged="$emit('reloadlist')"
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
}

</style>