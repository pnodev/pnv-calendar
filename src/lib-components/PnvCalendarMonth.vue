<script>
import dayjs from 'dayjs';
import weekday from 'dayjs/plugin/weekday';
import weekOfYear from 'dayjs/plugin/weekOfYear';

dayjs.extend(weekday);
dayjs.extend(weekOfYear);

export default {
	props: {
		selected: {
			type: String,
			default: dayjs().format('YYYY-MM-DD'),
		},
	},
	data() {
		return {
			selectedDate: dayjs(),
		};
	},

	computed: {
		days() {
			return [
				...this.previousMonthDays,
				...this.currentMonthDays,
				...this.nextMonthDays,
			];
		},

		today() {
			return dayjs().format('YYYY-MM-DD');
		},

		month() {
			return Number(this.selectedDate.format('M'));
		},

		year() {
			return Number(this.selectedDate.format('YYYY'));
		},

		numberOfDaysInMonth() {
			return dayjs(this.selectedDate).daysInMonth();
		},

		currentMonthDays() {
			return [...Array(this.numberOfDaysInMonth)].map((day, index) => {
				return {
					date: dayjs(`${this.year}-${this.month}-${index + 1}`).format(
						'YYYY-MM-DD'
					),
					isCurrentMonth: true,
				};
			});
		},

		previousMonthDays() {
			const firstDayOfTheMonthWeekday = this.getWeekday(
				this.currentMonthDays[0].date
			);
			const previousMonth = dayjs(`${this.year}-${this.month}-01`).subtract(
				1,
				'month'
			);

			// Cover first day of the month being sunday (firstDayOfTheMonthWeekday === 0)
			const visibleNumberOfDaysFromPreviousMonth = firstDayOfTheMonthWeekday
				? firstDayOfTheMonthWeekday - 1
				: 6;

			const previousMonthLastMondayDayOfMonth = dayjs(
				this.currentMonthDays[0].date
			)
				.subtract(visibleNumberOfDaysFromPreviousMonth, 'day')
				.date();

			return [...Array(visibleNumberOfDaysFromPreviousMonth)].map(
				(day, index) => {
					return {
						date: dayjs(
							`${previousMonth.year()}-${previousMonth.month() + 1}-${
								previousMonthLastMondayDayOfMonth + index
							}`
						).format('YYYY-MM-DD'),
						isCurrentMonth: false,
					};
				}
			);
		},

		nextMonthDays() {
			const lastDayOfTheMonthWeekday = this.getWeekday(
				`${this.year}-${this.month}-${this.currentMonthDays.length}`
			);

			const nextMonth = dayjs(`${this.year}-${this.month}-01`).add(1, 'month');

			const visibleNumberOfDaysFromNextMonth = lastDayOfTheMonthWeekday
				? 7 - lastDayOfTheMonthWeekday
				: lastDayOfTheMonthWeekday;

			return [...Array(visibleNumberOfDaysFromNextMonth)].map((day, index) => {
				return {
					date: dayjs(
						`${nextMonth.year()}-${nextMonth.month() + 1}-${index + 1}`
					).format('YYYY-MM-DD'),
					isCurrentMonth: false,
				};
			});
		},
	},

	methods: {
		getWeekday(date) {
			return dayjs(date).weekday();
		},

		selectDate(newSelectedDate) {
			this.selectedDate = newSelectedDate;
		},
	},

	render() {
		return this.$scopedSlots.default({
			days: this.days,
			selectedDate: this.selectedDate,
			today: this.today,
			selectDate: this.selectDate,
		});
	},
};
</script>
