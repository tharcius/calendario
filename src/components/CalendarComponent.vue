<template>
  <div class="container">
    <div class="row">
      <div class=col-12>
        <h2 class="float-left">Treinos</h2>
        <div class="float-right">
          <button class="btn btn-primary">Cadastrar novo treino</button>
        </div>
      </div>
    </div>
    <div class="card margem">
      <div class="card-header">
        <button class="btn float-left" @click="lastMonth"><i class="material-icons">arrow_back_ios</i></button>
        <span class="title">{{dateContext.format('MMMM [de] Y')}}</span>
        <button class="btn float-right" @click="nextMonth"><i class="material-icons">arrow_forward_ios</i></button>
      </div>
      <div class="row">
        <div class="col-sm dia" v-for="(day, dayIndex) in days" :key="dayIndex">
            {{day}}
        </div>
      </div>
      <div class="row">
        <template v-for="c in parseInt(firstDayOfMonth.format('d'))">
          <div class="col-sm dia" :key="c">&nbsp;</div>
        </template>
        <template v-for="day in daysInMonth">
          <div class="col-sm dia" :key="day">
            <div class="card data">
              <div class="card-body">
                <h5 class="card-title float-right">{{day}}º</h5>
                <p class="card-text">
                  <button type="button" class="btn btn-primary btn-sm botao" data-container="body" data-toggle="popover" data-trigger="focus" data-placement="top" data-content="Treino de Futebol." v-if="(day%6) == 0">
                    10:00 - 12:00
                  </button>
                  <button type="button" class="btn btn-primary btn-sm botao" data-container="body" data-toggle="popover" data-trigger="focus" data-placement="top" data-content="Treino de Ping-Pong." v-if="(day%2) == 0">
                    09:00 - 11:00
                  </button>
                  <button type="button" class="btn btn-primary btn-sm botao" data-container="body" data-toggle="popover" data-trigger="focus" data-placement="top" data-content="Treino de Volei." v-if="(day%5) == 0">
                    15:00 - 18:00
                  </button>
                </p>
              </div>
            </div>
          </div>
          <div class="w-100" v-if="((parseInt(firstDayOfMonth.format('d'))+day)%7) == 0"><span hidden>{{count = 0}}</span></div>
          <span hidden v-else="">{{count++}}</span>
        </template>
        <template v-for="c in (7-count)">
          <div class="col-sm dia" :key="c">&nbsp;</div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
moment.locale('pt-br', {
  weekdays: ['Domingo', 'Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado'],
  weekdaysShort: ['Dom', 'Seg', 'Ter', 'Qua', 'Qin', 'Sex', 'Sáb'],
  monthsShort: ['Jan', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'],
  months: ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'],
  longDateFormat: {
    LT: 'HH:mm',
    LTS: 'HH:mm:ss',
    L: 'DD/MM/YYYY',
    LL: 'D MMMM YYYY',
    LLL: 'D MMMM YYYY HH:mm',
    LLLL: 'dddd D MMMM YYYY HH:mm'
  }})
export default {
  name: 'CalendarComponent',
  data () {
    return {
      dateContext: moment(),
      days: ['Domingo', 'Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado'],
      today: moment(),
      count: 0
    }
  },
  methods: {
    nextMonth () {
      this.dateContext = this.addMonth
    },
    lastMonth () {
      this.dateContext = this.subtractMonth
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

.title{
  font-size: 1.5em;
  font-weight: bold;
}

.margem{
  padding: 1rem;
}

.dia, .card-body{
  padding: 0 .3rem;
  display: inline-grid;
}

.card-title{

}

.card-body{
  background-color: #f5f5f5;
}

.dia:hover{
  flex-grow: 1;
}
.data{
  height: 6rem;
  margin: .3rem 0;
  overflow: auto;
}

.botao{
  min-width: 70%;
  max-width: 70%;
  margin: 0 auto;
  padding: 0;
}
</style>
