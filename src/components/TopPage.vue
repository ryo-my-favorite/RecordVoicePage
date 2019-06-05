<template>
    <v-layout>
        <v-flex>
            <v-app>
                <div class="header-part">
                    <div>
                        <v-btn small v-on:click="startRecord">Start!</v-btn>
                        <v-btn small v-on:click="showResult">Result</v-btn>
                    </div>
                    <div>
                    </div>
                </div>
                <hr>
                <div>
                    <v-flex xs 12 sm6 offset-sm3>
                        <v-card class="letter"
                         min-height=360>
                            <div class="message">
                                <span>{{ recordMessage }}</span>
                            </div>
                        </v-card>
                    </v-flex>
                </div>
            </v-app>
        </v-flex>
    </v-layout>
</template>

<script>
    let SpeechRecognition = webkitSpeechRecognition || SpeechRecognition;
    const recognition = new SpeechRecognition();
    recognition.lang = 'ja-JP';
    recognition.interimResults = true;
    //recognition.continuous = true;
    let finalTranscript = '';

    
export default {
    data (){
        return{
            recordMessage: '',
            //finalTranscript: '',
            num: ''
        }
    },
    methods: {
        startRecord: function(){
            this.recordMessage = '';
            finalTranscript = '';
            let interimTranscript = ''
            recognition.start();
            recognition.onresult = (event) => {
                for(let i = event.resultIndex; i< event.results.length; i++){
                    let transcript = event.results[i][0].transcript;
                    if(event.results[i].isFinal){
                        finalTranscript = interimTranscript;
                        this.recordMessage = finalTranscript;
                    }else{
                        interimTranscript = transcript;
                        this.recordMessage = interimTranscript
                    }
                }
                this.num = this.recordMessage.match(/[らラ]/g || []);
            }
        },
        showResult: function(){
            finalTranscript = '';
            let number = (this.num === null) ? 0 : this.num.length;
            console.log(number + "回");
        }
    } 
}
</script>

<style>
    .header-part{
        margin-left: 32px;
    }
    .letter{
        margin-top: 32px;
    }
    .message{
        padding: 8px;
        min-height: 320px;
        white-space: pre-wrap;
    }
</style>
