<script>
import Vue from 'vue';
import { PnvCalendarMonth, PnvCalendarDateSelector, PnvCalendarDateIndicator, PnvCalendarWeekdays, PnvCalendarMonthDayItem } from '@/entry';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    PnvCalendarMonth,
    PnvCalendarDateSelector,
    PnvCalendarDateIndicator,
    PnvCalendarWeekdays,
    PnvCalendarMonthDayItem,
  }
});
</script>

<template>
  <div id="app">
    <PnvCalendarMonth v-slot="{ days, selectedDate, today, selectDate }">
			<div class="calendar">
				<PnvCalendarDateSelector
					v-slot="{ selectPrevious, selectCurrent, selectNext }"
					:current-date="today"
					:selected-date="selectedDate"
					@dateSelected="selectDate"
				>
					<div>
						<button @click="selectPrevious">Prev</button>
						<button @click="selectCurrent">Current</button>
						<button @click="selectNext">Next</button>
					</div>
				</PnvCalendarDateSelector>
				<PnvCalendarDateIndicator
					v-slot="{ selectedMonth }"
					:selected-date="selectedDate"
				>
					<div>
						{{ selectedMonth }}
					</div>
				</PnvCalendarDateIndicator>
				<PnvCalendarWeekdays v-slot="{ weekdays }">
					<ol>
						<li v-for="weekday in weekdays" :key="weekday">
							{{ weekday }}
						</li>
					</ol>
				</PnvCalendarWeekdays>
				<ol>
					<PnvCalendarMonthDayItem
						v-for="day in days"
						:key="day.date"
						v-slot="{ label }"
						:day="day"
					>
						<li>
							{{ label }}
						</li>
					</PnvCalendarMonthDayItem>
				</ol>
			</div>
		</PnvCalendarMonth>
  </div>
</template>

<style>
.calendar {
  max-width: 800px;
  margin: auto;
}
ol {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  grid-template-columns: repeat(7, minmax(0, 1fr));
}
li {
  padding: 2rem 1rem;
  border: 1px solid #ccc;
}
</style>
