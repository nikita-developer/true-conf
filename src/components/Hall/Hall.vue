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
			:steps="steps"
			:delay="delay"
			:duration="duration"
			:step="step"
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
				step: 3,
			}
		},
		methods: {
			paginationActive(index) {
				this.step = index
			},
		}
	}
</script>

<style lang="scss" scoped>
	@import 'styles/main.scss';
</style>