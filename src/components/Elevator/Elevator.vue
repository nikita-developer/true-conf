<template>
    <div class="elevator">
        <div
            :style="{
                bottom: bottom + '%',
                transition: seconds() + 's bottom linear',
                height: elevatorHeight() + '%',
            }"
            class="elevator__box"
        >
            <div class="elevator__info">{{info}}</div>
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
                info: 'Без работы',
                time: null
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
                return (this.time / 1000) %60
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

            // выводим информацию о местонахождении лифта)
            thisFloorInfo(oldFloor, newFloor, result) {
                oldFloor > newFloor ? result = oldFloor - newFloor : result = newFloor - oldFloor
                this.info = oldFloor
                newFloor > oldFloor ? this.info = oldFloor++ : this.info = oldFloor--

                let logInfo = setInterval(() => {
                    newFloor > oldFloor ? this.info = oldFloor++ : this.info = oldFloor--
                }, this.time / result)

                setTimeout(() => {
                    clearInterval(logInfo)
                }, this.time)
            },

            // 4 лифт по вызову =)
            nex_step(step, oldFloor) {

                // говорим что лифт занят
                this.is_finik = false

                // 5 говорим на какой этаж двигаться
                this.operation(step)

                oldFloor > step ? this.time = (oldFloor - step) * this.duration : this.time = (step - oldFloor) * this.duration

                // выводим информацию о местонахождении лифта)
                this.thisFloorInfo(oldFloor, step)

                // ждем
                setTimeout(() => {
                    this.info = "Жду"
                }, this.time + 500)

                setTimeout(() => {
                    // если в очереди еще есть вызовы, то выпоняем их
                    if(this.history.length) {
                        this.next_floor()
                    } else {
                        // если в очереди нет вызовов, то лифт чилит
                        this.is_finik = true
                    }
                    this.$emit('removeActivePagination', step)
                }, this.time + this.delay)
            },

            // 3 удаляем первый элемент и запускаем функцию
            next_floor() {
                const current_floor = this.history.shift()
                current_floor()
            }
        },
        watch: {
            step(newValue, oldValue) {
                // 1 пушим вызов лифта
                let counter = this.step
                this.history.push(() => this.nex_step(counter, oldValue))

                this.$emit('addActivePagination', counter)

                // 2 если лифт на расслабоне
                if(this.is_finik) {
                    this.next_floor()
                }
            }

        },
        mounted() {
            this.operation(this.step)
            this.seconds()
            this.elevatorHeight()
        }
    }
</script>

<style lang="scss" scoped>
    @import 'styles/main.scss';
</style>