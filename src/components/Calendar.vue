<template>
  <div>
    <CalendarSelector />
  <div class="container">
    <div class="calendar-week" v-for="(_,i) in 7">
      <span class="weeklyDay"
      :class="{weekEnd: i === 5 || i === 6}">{{ weekDayName(i) }}</span>
    </div>
    <div class="calendar-item" v-for="i in days">
      {{ i }}
    </div>
  </div>
  </div>
</template>

<script>
import getDaysOfMonth from "../composables/date-utils";
import getFirstWeekday from "../composables/week-days";
import CalendarSelector from "./CalendarSelector";

export default {
  name: "Calendar",
  components: {CalendarSelector},
  data() {
    const currentDay = new Date()
    const month = currentDay.getMonth()
    const year = currentDay.getFullYear()
    const daysInMonth = getDaysOfMonth(month, year)
    const firstDayIndex = getFirstWeekday(month, year)
    const days = []
    for (let i = firstDayIndex; i < daysInMonth + firstDayIndex; i++) {
      days[i] = i + 1 - firstDayIndex
    }
    return {
      days
    }
  },
  methods: {
    weekDayName(i) {
      const d = new Date('2021-04-05')
      d.setDate(d.getDate() + i)
      return d.toLocaleDateString('ru-RU', {weekday: 'short'})
    },
  },
}
</script>

<style scoped>
.container {

  display: grid;
  grid-template-columns: repeat(7, 1fr);
}
.calendar-week {
  margin-bottom: 20px;
  padding-left: 2px;
}
.weeklyDay {
  text-transform: uppercase;
  font-weight: bold;
}
.weekEnd {
  text-transform: uppercase;
  font-weight: bold;
  color: red;
}
.calendar-item {
  min-height: 32px;
  min-width: 32px;
  padding: 10px 10px 20px;
  display: flex;
  justify-content: end;
  align-items: start;
  transform-origin: 50% 50%;
  font-size: 18px;
  font-weight: bold;
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.17);
}
</style>;
