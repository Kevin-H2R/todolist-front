<template>
    <v-card class="task-row-loader animate-flicker" color="#EEE">
        <v-container class="task-row-loader__container"> 
            <v-layout row align-center>
                <v-flex xs1 offset-xs11>
                    <v-card-actions>
                        <v-btn class="task-row-loader__check-button"
                            fab dark small color="#FFF"
                        >
                            <v-icon dark>done</v-icon>
                        </v-btn>
                    </v-card-actions>
                </v-flex>
            </v-layout>
        </v-container>
    </v-card>
</template>
<script>
export default {
    
}
</script>
<style lang="scss">
    .task-row-loader {
        margin: 10px 0;
        padding: 0 5px 0 5px;
        border-radius: 50px !important;
        &__container {
            padding: 0;
        }
        &__check-button {
            width: 30px !important;
            height: 30px !important;
        }
    }
    @keyframes flickerAnimation { /* flame pulses */
        0%   { opacity:1; }
        50%  { opacity:0; }
        100% { opacity:1; }
    }
    .animate-flicker {
        opacity: 1;  
        animation: flickerAnimation 1500ms infinite;
    }
</style>


