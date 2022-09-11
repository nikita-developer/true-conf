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
				steps: null,
				delay: null,
				duration: null,
				step: null,
				addIsActivePagination: null,
				removeIsActivePagination: null,
				localStorageOption: null,
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
			localStorageOperations() {
				if(localStorage.getItem('Настройки лифта')) {
					this.steps = JSON.parse(localStorage.getItem('Настройки лифта')).steps
					this.delay = JSON.parse(localStorage.getItem('Настройки лифта')).delay
					this.duration = JSON.parse(localStorage.getItem('Настройки лифта')).duration
					this.step = JSON.parse(localStorage.getItem('Настройки лифта')).step
				} else {
					this.steps = 4
					this.delay = 3000
					this.duration = 1000
					this.step = 1
				}
			}
		},
		beforeMount() {
			this.localStorageOperations()
			this.hallRowHeight()
		},
	}
</script>

<style lang="scss" scoped>
	@import 'styles/main.scss';
</style>