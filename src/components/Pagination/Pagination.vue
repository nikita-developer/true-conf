<template>
    <div
        @click="eventActive"
        class="pagination"
        :class="{'active': isActive}"
    >
    </div>
</template>

<script>
    export default {
        data() {
            return {
                isActive: false,
            }
        },
        props: {
            index: Number,
            addIsActivePagination: Number,
            removeIsActivePagination: Number,
        },
        methods: {
            eventActive() {
                this.$emit('paginationActive', this.index + 1)
            },
        },
        watch: {
            addIsActivePagination() {
                if(this.addIsActivePagination == this.index + 1) {
                    this.isActive = true
                }
            },
            removeIsActivePagination() {
                if(this.removeIsActivePagination == this.index + 1) {
                    this.isActive = false
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import 'styles/main.scss';
</style>