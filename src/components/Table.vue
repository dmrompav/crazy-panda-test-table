<template lang="pug">
	table.table
		caption.caption {{ tableData.caption }}
		tr.header
			th.header__title.cell(
				v-for="(title, ind) in tableData.head"
				@click="$emit('sort', ind)"
			) 
				span.sort(v-if="typeOfSort[ind]" v-html="typeOfSort[ind]==='ascend'? '&uarr;' : '&darr;'") 
				| {{ title }}
		tr.main-row(
			v-for="row in tableDataCutted"
			:key="row[0]"
		)
			td.main-row__cell.cell(
				v-for="cell in row"
			) {{ cell }}
</template>



<script>
export default {
	name: "Table",
	props: {
		pageSelected: Number,
		quantity: Number,
		tableData: Object,
		typeOfSort: Array,
	},
	computed: {
		tableDataCutted() {
			if (this.tableData.main.length <= this.quantity) {
				return this.tableData.main
			}
			else {
				return this.tableData.main
					.slice((this.pageSelected - 1) * this.quantity, this.pageSelected * this.quantity)
			}
		}
	}
};
</script>



<style scoped lang="stylus">
.table
	border-collapse collapse
.caption
	font-size 28px
	font-weight bold
	
.cell
	border 1px solid black 
	text-align center
	padding 0 8px 0 4px
	max-width 600px
	word-break break-word
.header
	&__title
		background #6666bb
		cursor pointer
		user-select none
		&:hover
			background #7777cc

</style>
