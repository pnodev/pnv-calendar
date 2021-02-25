<script>
const WEEKDAYS = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

export default {
  props: {
    weekdays: {
      type: Array,
      default(){
        return WEEKDAYS;
      }
    }
  },
	render() {
		return this.$scopedSlots.default({
			weekdays: this.weekdays,
		});
	},
};
</script>
