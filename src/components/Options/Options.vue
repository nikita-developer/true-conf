<template>
    <form class="options">
        <div class="options__title">Настройки лифта</div>
        <label class="options__label">
            <p class="options__text">Количество этажей</p>
            <input min="2" class="options__field" type="number">
        </label>
        <label class="options__label">
            <p class="options__text">Скорость лифта</p>
            <input min="1" class="options__field" type="number">
        </label>
        <label class="options__label">
            <p class="options__text">Сколько лифт будет ждать</p>
            <input min="1" class="options__field" type="number">
        </label>
        <label class="options__label">
            <p class="options__text">Начальный этаж лифта</p>
            <input min="1" class="options__field" type="number">
        </label>
        <button class="options__btn">Применить</button>
    </form>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
    @import 'styles/options.scss';
</style>