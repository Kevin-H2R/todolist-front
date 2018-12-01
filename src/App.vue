<template>
  <v-app>
    <v-content  class="main-app">
      <v-container>
        <v-slide-y-transition mode="out-in">
          <v-layout column>
            <v-layout row wrap justify-center>
            <v-flex xs12 md6>
              <new-task-input/>
              <v-card class="main-app__card" color="#F8F8F8">
                <v-container>
                  <date-slider/>
                  <!-- <v-slide-y-transition mode="out-in"> -->
                    <transition name="slide-fade">
                    <div v-if="this.items.length > 0">
                      <task-row v-for="(item, index) in this.items" :key="index" v-bind="item"/>
                    </div>
                    </transition>

                  <!-- </v-slide-y-transition> -->
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
  import NewTaskInput from './components/NewTaskInput'
  import axios from 'axios'
  import qs from 'qs'
  import { EventBus } from './js/eventbus.js'

  export default {
    components: {
      TaskRow,
      DateSlider,
      NewTaskInput
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

.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateY(-10px);
  opacity: 0;
}

</style>

