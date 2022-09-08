<template>
	<div class="hall">
		<div class="hall__row"
			v-for="(step, index) in steps"
			:key="step"
		>
			<Pagination
				@paginationActive="paginationActive"
				:index="index"
				class="hall__pagination"
			>
			</Pagination>
		</div>
		<Elevator
			v-for="elevator in elevators"
			:key="elevator.id"
			:steps="steps"
			:delay="delay"
			:duration="duration"
			:pagination_counter="pagination_counter"
			:elevator="elevator"
			class="hall__elevator"
		>
		</Elevator>
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
				pagination_counter: 1,
				elevators: [
					{
						id: 0,
						step: 0,
					}
				]
			}
		},
		methods: {
			paginationActive(index) {
				this.pagination_counter = index
			}
		}
	}
</script>

<style lang="scss" scoped>
	@import 'styles/main.scss';
</style>