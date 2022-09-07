<template>
	<div class="hall">
		<div class="hall__row">
			<Pagination class="hall__pagination"></Pagination>
		</div>
		<div class="hall__row">
			<Pagination class="hall__pagination"></Pagination>
		</div>
		<div class="hall__row">
			<Pagination class="hall__pagination"></Pagination>
		</div>
		<div class="hall__row">
			<Pagination class="hall__pagination"></Pagination>
		</div>
		<div class="hall__row">
			<Pagination class="hall__pagination"></Pagination>
		</div>
		<Elevator class="hall__elevator"></Elevator>
	</div>
</template>

<script>
	import Elevator from '../Elevator/Elevator.vue';
	import Pagination from '../Pagination/Pagination.vue';
	export default {
		components: {
			Elevator,
			Pagination
		}
	}
</script>

<style lang="scss" scoped>
	@import 'styles/main.scss';
</style>