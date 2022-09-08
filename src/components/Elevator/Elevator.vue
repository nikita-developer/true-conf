<template>
    <div class="elevator">
        <div :style="{bottom: height + '%'}" class="elevator__box"></div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                height: 0
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
			pagination_counter: {
                type: Number,
                default: 1,
            },
            elevator: {
                type: Object,
                default: {},
            },
        },
        methods: {
            elevatorEvents() {
                let result = 0
                for (let i = 1; i < this.pagination_counter; i++) {
                    result = result + 100 / this.steps
                }
                console.log(result);
                return this.height = result;
            }
        },
        watch: {
            pagination_counter: function () {
                this.elevatorEvents()
            }
        },
    }
</script>

<style lang="scss" scoped>
    @import 'styles/main.scss';
</style>