<template>
    <v-card class="task-row" hover tile>
        <v-container class="task-row__container"> 
            <v-layout row align-center @click="toggleCheckedState">
                <v-flex xs11>
                    <v-card-title class="task-row__title" :class="checked ? 'task-row__title--done' : ''" style="padding: 5px 10px">
                        {{ this.name }}
                    </v-card-title>
                </v-flex>
                <v-flex xs1>
                    <v-card-actions>
                        <v-btn width="30px" height="30px" class="task-row__check-button"
                            fab dark small color="success"
                            v-if="checked">
                            <v-icon dark>done</v-icon>
                        </v-btn>
                        <v-btn class="task-row__check-button"
                            flat icon color="grey lighten-2" v-else>
                            <v-icon>done</v-icon>
                        </v-btn>
                    </v-card-actions>
                </v-flex>
            </v-layout>
        </v-container>
    </v-card>
</template>
<script>
import axios from 'axios'
import qs from 'qs'
import { url } from '../js/database.js'

export default {
    name: 'task-row',
    props: {
        id: {
            type: Number,
            required: true
        },
        name: {
            type: String,
            required: true
        },
        done: {
            type: Boolean,
            required: true
        },
    },
    methods: {
        toggleCheckedState: function () {
            this.checked = !this.checked
            axios.post(url + 'tasks/check/', qs.stringify({id: this.id}))
            .then(function (response) {
            })
            .catch(function (error){
                console.log(error)
                this.checked = !this.checked
            })
        }
    },
    data: function () {
        return {
            checked: this.done,
            hovered: false
        }
    }
}
</script>
<style lang="scss">
    .task-row {
        margin: 10px 0;
        padding: 0 5px 0 5px;
        border-radius: 50px !important;
        &__container {
            padding: 0;
        }
        &__title {
            transition: all ease-in-out 200ms;
            font-size: 20px;
        }
        &__title--done {
            color: #CCC;
            text-decoration: line-through;
        }
        &__check-button {
            width: 30px !important;
            height: 30px !important;
        }
    }
</style>


