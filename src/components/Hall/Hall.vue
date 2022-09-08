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
		<Elevator v-for="elem in elevators" :key="elem.id" class="hall__elevator"></Elevator>
	</div>
</template>

<script>
	import Elevator from '../Elevator/Elevator.vue';
	import Pagination from '../Pagination/Pagination.vue';
	export default {
		components: {
			Elevator,
			Pagination
		},
		data() {
			return {
				steps: 5,
				delay: 3000,
				duration: 1000,
				elevators: [
					{
						id: 0,
						step: 0,
					}
				]
			}
		}
	}
</script>

<style lang="scss" scoped>
	@import 'styles/main.scss';
</style>