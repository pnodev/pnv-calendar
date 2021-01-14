<script>
import dayjs from 'dayjs';

export default {
	props: {
		day: {
			type: Object,
			required: true,
		},
	},

	computed: {
		label() {
			return dayjs(this.day.date).format('D');
		},
	},

	render() {
		return this.$scopedSlots.default({
			label: this.label,
		});
	},
};
</script>
