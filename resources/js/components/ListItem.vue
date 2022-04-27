<template>
    <div>
        <!-- {{item}} -->
        {{item.id}}
        {{item.task_name}}
        {{item.task_description}}
        {{item.user_name}}
    </div>
</template>

<script>
    export default {
        props: ['item']
    }
</script>