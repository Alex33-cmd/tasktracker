<template>
    <div>
        {{item.id}}
        {{item.task_name}}
    </div>
</template>

<script>
    export default {
        props: ['item']
    }
</script>