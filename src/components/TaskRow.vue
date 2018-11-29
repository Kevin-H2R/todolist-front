<template>
    <v-card class="task-row" hover tile>
        <v-container class="task-row__container"> 
            <v-layout row align-center @click="checked = !checked">
                <v-flex xs11>
                    <v-card-title class="task-row__title" :class="checked ? 'task-row__title--done' : ''">
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
        margin: 20px 0;
        padding: 0 25px 0 15px;
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


