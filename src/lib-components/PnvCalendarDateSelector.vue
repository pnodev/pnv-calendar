<script>
import dayjs from 'dayjs';

export default {
	props: {
		currentDate: {
			type: String,
			required: true,
		},

		selectedDate: {
			type: Object,
			required: true,
		},
	},

	methods: {
		selectPrevious() {
			const newSelectedDate = dayjs(this.selectedDate).subtract(1, 'month');
			this.$emit('dateSelected', newSelectedDate);
		},

		selectCurrent() {
			const newSelectedDate = dayjs(this.currentDate);
			this.$emit('dateSelected', newSelectedDate);
		},

		selectNext() {
			const newSelectedDate = dayjs(this.selectedDate).add(1, 'month');
			this.$emit('dateSelected', newSelectedDate);
		},
	},

	render() {
		return this.$scopedSlots.default({
			selectPrevious: this.selectPrevious,
			selectCurrent: this.selectCurrent,
			selectNext: this.selectNext,
		});
	},
};
</script>
