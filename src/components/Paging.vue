<template lang="pug">
	.paging
		.page-selector(
			v-if="multiSelect"
		)
			label(for="select1").page-selector__label Отображать по: 
			select#select1.page-selector__page-max.selector
					option(
						v-for="opt in pageMax"
						:selected="opt===50"
						@click="$emit('quantity', opt)"
					) {{ opt }}
		.page-selector
			label(for="select2").page-selector__label Страница: 
			button.page-selector__btn.btn(
				v-if="pageSelected > 1"
				@click="$emit('page-select', pageSelected - 1)"
			) <
			select#select2.page-selector__select.selector 
				option(
					v-for="i in howMuchPages"
					@click="$emit('page-select', i)"
					:selected="i===pageSelected"
				) {{ i }}
			button.page-selector__btn.btn(
				v-if="pageSelected < howMuchPages"
				@click="$emit('page-select', pageSelected + 1)"
			) >
</template>



<script>
export default {
	name: 'Paging',
	props: {
		multiSelect: Boolean,
		pageSelected: Number,
		tableLength: Number,
		quantity: Number
	},
	data() {
		return {
			pageMax: [10, 20, 50, 100]
		}
	},
	computed: {
		howMuchPages() {return Math.ceil(this.tableLength / this.quantity)}
	}
}
</script>



<style scoped lang="stylus">
.paging
	margin-top 6px

.btn
	height 20px
	border 1px solid black 
	padding 0 2px
	background #6666bb
	&:hover
		background #7777cc

.selector
	height 20px
	border 1px solid black

</style>
