<template>
    <v-layout row align-center class="date-slider">
        <v-flex xs1>
            <v-btn flat icon color="primary" @click="goToYesterday">
                <v-icon>keyboard_arrow_left</v-icon>
            </v-btn>
        </v-flex>
        <v-flex xs10 class="date-slider__date">
            <v-dialog
                ref="dialog"
                v-model="modal"
                :return-value.sync="currentDate"
                lazy
                full-width
                width="290px"
            >
                <div
                    slot="activator"
                    class="date-slider__text-field"
                >
                    {{ computedDateFormatted }}
                </div>
                <v-date-picker v-model="currentDate" scrollable locale="fr-FR">
                </v-date-picker>
            </v-dialog>
        </v-flex>
        <v-flex xs1 class="date-slider__right-arrow">
            <v-btn flat icon color="primary" @click="goToTomorrow">
                <v-icon>keyboard_arrow_right</v-icon>
            </v-btn>
        </v-flex>
    </v-layout>
</template>
<script>

import { EventBus } from '../js/eventbus.js'

export default {
    name: 'date-slider',
    computed: {
        computedDateFormatted: function () {
            return this.formatDate(this.currentDate)
        }
    },
    watch: {
        currentDate: function (value) {
            this.formattedDate = this.formatDate(this.currentDate)
            this.$refs.dialog.save(this.currentDate)
            this.modal = false
            EventBus.$emit('date-changed', this.currentDate);
        }
    },
    methods: {
        formatDate: function (date) {
            if (!date) return null

            const [year, month, day] = date.split('-')
            return `${('0' + day).slice(-2)}/${month}/${year}`
        },
        parseDate: function (date) {
            return date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + ('0' + date.getDate()).slice(-2)
        },
        goToTomorrow: function () {
            const date = new Date(this.currentDate);
            const tomorrow = new Date(date.getTime());
            tomorrow.setDate(date.getDate() + 1)
            this.currentDate = this.parseDate(tomorrow);
        },
        goToYesterday: function () {
            const date = new Date(this.currentDate);
            const yesterday = new Date(date.getTime());
            yesterday.setDate(date.getDate() - 1)
            this.currentDate = this.parseDate(yesterday);
        }
    },
    data: function () {
         var options = {
            year: "numeric",
            month: "2-digit",
            day: "numeric"
        };
        return {
            currentDate: this.parseDate(new Date()),
            formattedDate: null,
            modal: false
        }
    }
}
</script>
<style lang="scss" scoped>
    .date-slider {
        background-color: #F2F2F2;
        &__right-arrow {
            text-align: right;
        }
        &__text-field {
            text-align: center;
            font-weight: 500;
        }
    }
</style>


