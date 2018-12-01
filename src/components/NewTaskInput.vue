<template>
    <v-card class="newtask-input">
        <v-container class="newtask-input__container">
            <v-layout row align-center>
                <v-flex xs11>
                    <v-text-field
                        name="newTask"
                        id="newtask-input"
                        placeholder="What amazing think are you going to do?"
                        v-model="taskName"
                    ></v-text-field>
                </v-flex>
                <v-flex xs1>
                    <v-card-actions>
                        <v-fade-transition>
                            <v-btn fab dark small color="green"  v-show="taskName.length > 0"
                                class="newtask-input__button"
                                @click="addTask"
                                >
                                <v-icon>add</v-icon>
                            </v-btn>
                        </v-fade-transition>
                    </v-card-actions>
                </v-flex>
            </v-layout>
        </v-container>
    </v-card>
</template>
<script>
import axios from 'axios'
import qs from 'qs'
export default {
    name: 'new-task-input',
    methods: {
        addTask: function () {
            axios.post('http://localhost:8080/todolist/api/tasks/create', qs.stringify({name: this.taskName}))
            .then(function (response) {
                // adds created class in parent list
            })
            .catch(function (error) {
                console.log(error)
            })
        }
    },
    data: function () {
        return {
            taskName: ""
        }
    }
}
</script>
<style lang="scss" scoped>
    .newtask-input {
        margin-bottom: 24px;
        &__container {
            padding: 0 10px;
        }

        &__button {
            width: 30px !important;
            height: 30px !important;
        }
    }
</style>


