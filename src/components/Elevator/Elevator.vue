<template>
    <div class="elevator">
        <div
            :style="{
                bottom: bottom + '%',
                transition: seconds() + 's bottom linear',
                height: elevatorHeight() + '%',
            }"
            class="elevator__box">
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                bottom: 0,
                is_finik: true,
                history: [],
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
            // миллисекунды в секунды
            seconds() {
                return (this.duration / 1000) %60
            },

            // высота лифта
            elevatorHeight() {
                return 100 / this.steps
            },

            // что-то сложное которое говорит на сколько процентов подниматься
            operation(step) {
                let result = 0;
                for (let i = 1; i < step; i++) {
                    result = result + 100 / this.steps
                }
                return this.bottom = result
            },

            // 4 лифт по вызову =)
            nex_step(step) {

                // говорим что лифт занят
                this.is_finik = false

                // 5 говорим на какой этаж двигаться
                this.operation(step)

                setTimeout(() => {
                    // если в очереди еще есть вызовы, то выпоняем их
                    if(this.history.length) {
                        this.next_floor()
                    } else {
                        // если в очереди нет вызовов, то лифт чилит
                        this.is_finik = true
                    }
                }, this.delay)
            },

            // 3 удаляем первый элемент и запускаем функцию
            next_floor() {
                const current_floor = this.history.shift()
                current_floor()
            }
        },
        watch: {
            step() {
                // 1 пушим вызов лифта
                let counter = this.step
                this.history.push(() => this.nex_step(counter))

                // 2 если лифт на расслабоне
                if(this.is_finik) {
                    this.next_floor()
                }
            }

        },
    }
</script>

<style lang="scss" scoped>
    @import 'styles/main.scss';
</style>