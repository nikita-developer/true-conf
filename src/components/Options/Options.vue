<template>
    <form class="options" @submit.prevent="readyOptions">
        <div class="options__title">Настройки лифта</div>
        <label class="options__label">
            <p class="options__text">Количество этажей</p>
            <input
                min="2"
                class="options__field"
                type="number"
                v-model="newSteps"
            >
        </label>
        <label class="options__label">
            <p class="options__text">Сколько лифт будет ждать</p>
            <input
                min="1000"
                step="1000"
                class="options__field"
                type="number"
                v-model="newDelay"
            >
        </label>
        <label class="options__label">
            <p class="options__text">Скорость лифта</p>
            <input
                min="1000"
                step="1000"
                class="options__field"
                type="number"
                v-model="newDuration"
            >
        </label>
        <label class="options__label">
            <p class="options__text">Начальный этаж лифта</p>
            <input
                min="1"
                :max="steps"
                class="options__field"
                type="number"
                v-model="newStep"
            >
        </label>
        <button class="options__btn">Применить</button>
    </form>
</template>

<script>
    export default {
        props: ["steps", "delay", "duration", "step"],
        data() {
            return {
                newSteps: this.steps,
				newDelay: this.delay,
				newDuration: this.duration,
				newStep: this.step,
            }
        },
        methods: {
            readyOptions() {
                let dataOptions = {
                    steps: this.newSteps,
                    delay: this.newDelay,
                    duration: this.newDuration,
                    step: this.newStep,
                }
                this.$emit('newDataOptions', dataOptions)

                var optionsData = {
                    steps: this.newSteps,
                    delay: this.newDelay,
                    duration: this.newDuration,
                    step: this.newStep,
                };
                localStorage.setItem('Настройки лифта', JSON.stringify(optionsData) );
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import 'styles/options.scss';
</style>