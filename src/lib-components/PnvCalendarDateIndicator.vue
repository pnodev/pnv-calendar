<script>
export default {
	props: {
		selectedDate: {
			type: Object,
			required: true,
		},
	},

	computed: {
		selectedMonth() {
			return this.selectedDate.format('MMMM YYYY');
		},
	},

	render() {
		return this.$scopedSlots.default({
			selectedMonth: this.selectedMonth,
		});
	},
};
</script>
