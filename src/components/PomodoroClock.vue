<template>
    <v-card class="mt-8">
        <v-tabs v-model="timerType" grow>
            <v-tab
                v-for="tab in tabsTitles"
                :key="tab"
            >
                {{ tab }}
            </v-tab>
        </v-tabs>
            <v-window v-model="timerType">
                <v-window-item>
                     <v-card 
                        class="pa-5 d-flex flex-column justify-center align-center"
                        flat
                     >
                     <h1 class="time">{{ displayMinutes }}:{{ displaySeconds }}</h1>
                     <div class="button-group">
                        <v-btn @click="start"  color="primary">
                            <v-icon left small>mdi-play-circle-outline</v-icon>
                            Start
                        </v-btn>
                        <v-btn @click="stop" color="error">
                            <v-icon left small>mdi-stop-circle-outline</v-icon>
                            Stop
                        </v-btn>
                        <v-btn @click="reset" :disabled="timerIsRunnin">
                            <v-icon left small>mdi-restart</v-icon>
                            Reset
                        </v-btn>
                    </div>
                     </v-card>    
                </v-window-item>
            </v-window>
    </v-card>
</template>
<script>
export default{
    data(){
        return{
            timerIsRunnin:false,
            timerInstance: null,
            totalSeconds: 25 * 60,
            timerType:0,
            tabsTitles: ['Pomodoro','Short break','Long Break']
        }
    },
    computed:{
        displayMinutes(){
            const minutes = Math.floor(this.totalSeconds/60)
            return this.formatTime(minutes)
        },
        displaySeconds(){
            let seconds = this.totalSeconds % 60
            return this.formatTime(seconds)
        },
    },
    methods:{
        formatTime(time){ //Создаётся что бы во время работы таймера цифры не сьезжали.
            if (time < 10){
                return '0' + time
            }
            return time.toString()
        },
        start(){
            this.stop()
            this.timerIsRunnin = true
            this.timerInstance = setInterval(()=>{
                this.totalSeconds -=1
            },1000)
        },
        stop(){
            this.timerIsRunnin = false
            clearInterval(this.timerInstance)
        },
        reset(){
            this.stop(),
            this.totalSeconds = 25*60
        }
    }
}
</script>
<style>
.v-card{
    width: 600px;
}
.time{
    font-size: 80px;
    font-weight: 400;
    text-align: center;
}
.v-btn{
    margin: 0 2px;
}
</style>