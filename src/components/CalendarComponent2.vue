<template>
  <div class="calendar">
    <div class="calendar-header">
      <i class="fa fa-fw fa-chevron-left" @click="subtractMonth"></i>
      <h4>{{month + ' - ' + year}}</h4>
      <i class="fa fa-fw fa-chevron-right" @click="addMonth"></i>
    </div>
    <div class="container">
      <div class="row">
        <div class="col-sm" v-for="(day, key) in days" :key="key">
          {{day}}
        </div>
      </div>
      <div class="row">
        <div v-for="(date, key) in daysInMonth"
          class="col-sm"
          :key="key"
          :class="{'current-day': date == initialDate && month == initialMonth && year == initialYear}">
          {{date}}
          <div class="w-100" v-if="(key+1)%7 == 0">{{key+1}}</div>
        </div>
      </div>
    </div>
    <br>{{firstDayOfMonth.format('d')}}
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'CalendarComponent',
  data () {
    return {
      dateContext: moment(),
      days: ['Domingo', 'Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado'],
      today: moment()
    }
  },
  computed: {
    year: function () {
      return this.dateContext.format('Y')
    },
    month: function () {
      return this.dateContext.format('MMMM')
    },
    daysInMonth: function () {
      return this.dateContext.daysInMonth()
    },
    currentDate: function () {
      return this.dateContext.get('date')
    },
    firstDayOfMonth: function () {
      let t = this
      return moment(t.dateContext).subtract((t.currentDate - 1), 'days')
    },
    initialDate: function () {
      return this.today.get('date')
    },
    initialMonth: function () {
      return this.today.format('MMMM')
    },
    initialYear: function () {
      return this.today.format('Y')
    },
    addMonth: function () {
      return moment(this.dateContext).add(1, 'month')
    },
    subtractMonth: function () {
      return moment(this.dateContext).subtract(1, 'month')
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.current-day{
  color: red;
}
</style>
