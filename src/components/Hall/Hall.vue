<template>
	<div class="hall">
		<div class="hall__row"
			v-for="(step, index) in steps"
			:key="step"
			:style="{height: hallRowHeight() + '%'}"
		>
			<Pagination
				@paginationActive="paginationActive"
				:addIsActivePagination="addIsActivePagination"
				:removeIsActivePagination="removeIsActivePagination"
				:index="index"
				class="hall__pagination"
			>
			</Pagination>
		</div>
		<Elevator
			@addActivePagination="addActivePagination"
			@removeActivePagination="removeActivePagination"
			:steps="steps"
			:delay="delay"
			:duration="duration"
			:step="step"
			class="hall__elevator"
		>
		</Elevator>
		<Options
			@newDataOptions="newDataOptions"
			:steps="steps"
			:delay="delay"
			:duration="duration"
			:step="step"
			class="hall__options"
		></Options>
	</div>
</template>

<script>
	import Elevator from '../Elevator/Elevator.vue';
	import Pagination from '../Pagination/Pagination.vue';
	import Options from '../Options/Options.vue';
	export default {
		components: {
			Elevator,
			Pagination,
			Options
		},
		data() {
			return {
				steps: 8,
				delay: 3000,
				duration: 1000,
				step: 1,
				addIsActivePagination: null,
				removeIsActivePagination: null,
			}
		},
		methods: {
			paginationActive(index) {
				this.step = index
			},
			addActivePagination(step) {
				this.addIsActivePagination = step
			},
			removeActivePagination(step) {
				this.removeIsActivePagination = step
			},
			newDataOptions(newOptions) {
				this.steps = newOptions.steps
				this.delay = newOptions.delay
				this.duration = newOptions.duration
				this.step = newOptions.step
			},
			hallRowHeight() {
                return 100 / this.steps
            },
		},
		mounted() {
            this.hallRowHeight()
        }
	}
</script>

<style lang="scss" scoped>
	@import 'styles/main.scss';
</style>