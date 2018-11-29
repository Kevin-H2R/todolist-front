<template>
  <v-app>
    <!-- <v-toolbar fixed app>
      <v-spacer></v-spacer>
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar> -->
    <v-content  class="main-app">
      <v-container>
        <v-slide-y-transition mode="out-in">
          <v-layout column>
            <v-layout row wrap justify-center>
            <v-flex xs12 md6>
              <div style="text-align: center">
                <img src="/public/v.png" alt="Vuetify.js" class="mb-5" />
              </div>
              <v-card class="main-app__card" color="#F8F8F8">
                <v-container>
                  <date-slider/>
                  <task-row v-for="(item, index) in this.items" :key="index" v-bind="item"/>
                  <div style="left: 50%; position: absolute; margin-top: 16px">
                    <v-btn
                      color="green"
                      dark
                      bottom
                      fab
                      style="left: -50%"
                    >
                      <v-icon>add</v-icon>
                    </v-btn>
                  </div>
                </v-container>
              </v-card>
            </v-flex>
            </v-layout>
          </v-layout>
        </v-slide-y-transition>
      </v-container>
    </v-content>
  
    <v-footer fixed app>
      <span>&copy; H2R</span>
    </v-footer>
  </v-app>
</template>

<script>
  import TaskRow from './components/TaskRow'
  import DateSlider from './components/DateSlider'
  import axios from 'axios'
  import qs from 'qs'
  import { EventBus } from './js/eventbus.js'

  export default {
    components: {
      TaskRow,
      DateSlider
    },
    created: function () {
      const today = new Date();
      const formattedDate = today.getFullYear() + '/' + (today.getMonth() + 1) + '/' + today.getDate()
      axios.post('http://localhost:8080/todolist/api/tasks/', qs.stringify({date: formattedDate}))
      .then((response) => {
        this.items = response.data
      })
      .catch(function (error) {
        console.log(error)
      })
      var self = this
      EventBus.$on('date-changed', function (currentDate) {
        self.updateList(currentDate)
      })
    },
    methods: {
      updateList: function (currentDate) {
        var that = this
        axios.post('http://localhost:8080/todolist/api/tasks/', qs.stringify({date: currentDate}))
        .then(function (response) {
          that.items = response.data
        })
        .catch(function (error) {
            console.log(error)
        })
      }
    },
    data () {
      return {
        title: 'H2R Todolist',
        items: []
      }
    }
  }
</script>
<style lang="scss">

  .main-app {
    &__card {
      padding: 20px 15px;
      margin-bottom: 20px;
    }
  }

  .v-content {
    background-image: linear-gradient(#8fbff5, #4b87cc);
  }

  .v-text-field > .v-input__control > .v-input__slot:before {
    border: none;
  }

</style>

