<template>
    <div class="pagination" @click="eventActive"></div>
</template>

<script>
    export default {
        emits: ['paginationActive'],
        props: {
            index: Number,
        },
        methods: {
            eventActive() {
                this.$emit('paginationActive', this.index + 1)
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import 'styles/main.scss';
</style>