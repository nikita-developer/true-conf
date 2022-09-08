<template>
    <div class="elevator">
        <div :style="{bottom: height + '%'}" class="elevator__box"></div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                height: 0,
            }
        },
        props: {
            steps: {
                type: Number,
                default: 5,
            },
            delay: {
                type: Number,
                default: 3000,
            },
			duration: {
                type: Number,
                default: 1000,
            },
            step: {
                type: Number,
                default: 1,
            },
        },
        methods: {
            elevatorEvents(result = 0) {
                for (let i = 1; i < this.step; i++) {
                    result = result + 100 / this.steps
                }
                return this.height = result
            }
        },
        watch: {
            step() {
                this.elevatorEvents()
            }
        },
        mounted() {
            this.elevatorEvents()
        },
    }
</script>

<style lang="scss" scoped>
    @import 'styles/main.scss';
</style>