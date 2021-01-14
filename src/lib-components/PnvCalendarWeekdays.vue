<script>
const WEEKDAYS = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

export default {
	computed: {
		weekdays() {
			return WEEKDAYS;
		},
	},
	render() {
		return this.$scopedSlots.default({
			weekdays: this.weekdays,
		});
	},
};
</script>
