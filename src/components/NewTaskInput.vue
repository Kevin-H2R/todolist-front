<template>
    <v-card class="newtask-input">
        <v-container class="newtask-input__container">
            <v-layout row align-center>
                <v-flex xs11>
                    <v-text-field
                        name="newTask"
                        id="newtask-input"
                        placeholder="What amazing think are you going to do?"
                        v-model="text"
                    ></v-text-field>
                </v-flex>
                <v-flex xs1>
                    <v-card-actions>
                        <v-fade-transition>
                            <v-btn fab dark small color="green"  v-show="text.length > 0"
                                class="newtask-input__button"
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
export default {
    name: 'new-task-input',
    data: function () {
        return {
            text: ""
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


