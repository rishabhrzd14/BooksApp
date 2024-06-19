<template>
    <div class='listHeader'>
    {{data.Title}}
    </div>
</template>

<script setup>
const props = defineProps({
    data: {
        type:Object,
        default: {}
    }
})
    
</script>

<style scoped>
.listHeader{
display : flex
}
</style>