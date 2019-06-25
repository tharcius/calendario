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
        <button class="btn float-left" @click="lastMonth"><i class="material-icons">Mês Anterior</i></button>
        <span class="title">{{dateContext.format('MMMM [de] Y')}}</span>
        <button class="btn float-right" @click="nextMonth"><i class="material-icons">Próximo Mês</i></button>
      </div>
      <div class="row">
        <div class="col-sm dia" v-for="(day, dayIndex) in days" :key="dayIndex">
            {{day}}
        </div>
      </div>
      <div class="row">
        <template v-for="c in parseInt(firstDayOfMonth.format('d'))">
          <div class="col-sm dia">&nbsp;<span hidden>{{c}}</span></div>
        </template>

        <template v-for="(day, key) in daysInMonth">
          <div class="col-sm dia" :key="key">
            <div class="card data">
              <div class="card-body">
                <h5 class="card-title float-right">{{day}}º</h5>
                <p class="card-text">&nbsp;{{isSaturday(day)}} <br> {{diaDaSemana(day)}}</p>
              </div>
            </div>
          </div>
          <div class="w-100" v-if="isSaturday(day)"><span hidden>{{count = 0}}</span></div>
        </template>
        <template v-for="c in (7-count)">
          <div class="col-sm dia">&nbsp;<span hidden>{{c}}</span></div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
moment.locale('pt-br')
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
    },
    isSaturday (day) {
      let month = this.dateContext.format('MM')
      let year = this.dateContext.format('YYYY')
      let dia = `${year}-${month}-${parseInt(day)}`
      if (parseInt(moment(dia).format('d')) == 6) {
        return true
      }
      return false
    },
    diaDaSemana (day) {
      let month = this.dateContext.format('MM')
      let year = this.dateContext.format('YYYY')
      let dia = `${year}-${month}-${parseInt(day)}`
      return moment(dia).format('dd DD-MM-YYYY')
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
