<template>
  <div>
    <v-card>
      <v-container grid-list-lg>
        <v-layout row wrap>
          <v-flex xs6 v-for="data in onayamiTickets" :key="data.id">
            <v-card color="primary" class="white--text">
              <v-card-title primary-title>
                <div>{{ data.name }}</div>
                <div>{{ data.createdAt|printDate }}</div>
              </v-card-title>
              <v-card-text>
                <div>{{ data.content }}</div>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-card>
  </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'

export default {
  name: 'TicketIndex', 
  filters: {
    printDate (val) {
      return moment(val).locale('ja').format('YYYY年MM月DD日(ddd) HH時mm分ss秒')
    },
  },

  data () {
    return {
      onayamiTickets: [],
    }
  },
  methods: {
    fetchData () {
      axios.get('http://localhost:8000/api/1.0/tickets/freeticket/').then(res => {
        console.log(res)
        this.onayamiTickets = res.data.results
      })
    },
  },
  mounted () {
    this.fetchData()
  },
}
</script>
