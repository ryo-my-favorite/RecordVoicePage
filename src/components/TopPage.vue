<template>
    <v-layout>
        <v-flex>
            <v-app>
                <div class="header-part">
                    <h1>Microphone Test</h1>   
                    <div>
                        <v-btn small v-on:click="startRecord">Start Record</v-btn>
                        <v-btn small v-on:click="stopRecord">Stop Record</v-btn>
                    </div>
                    <div>
                        <v-flex xs12 sm3 md3>
                            <v-text-field
                            v-model="sendTo"
                            placeholder="To">
                            </v-text-field>
                        </v-flex>
                        <v-flex xs12 sm3 md3>
                            <v-text-field
                            v-model="sendFrom"
                            placeholder="From">
                            </v-text-field>
                        </v-flex>
                    </div>
                </div>
                <hr>
                <div>
                    <v-flex xs 12 sm6 offset-sm3>
                        <v-card class="letter"
                         min-height=360>
                            <div class="send-to">{{ "To " + sendTo }}</div>
                            <div class="message">{{ recordMessage }}</div>
                            <div class="send-from">{{ "From " + sendFrom }}</div>
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
    recognition.continuous = true;

    let finalTranscript = '';

    
export default {
    data (){
        return{
            recordMessage: '',
            sendTo: '',
            sendFrom: ''
        }
    },
    methods: {
        startRecord: function(){
            this.recordMessage = "";
            recognition.start();
            recognition.onresult = (event) => {
                let interimTranscript = '';
                for(let i = event.resultIndex; i< event.results.length; i++){
                let transcript = event.results[i][0].transcript;
                if(event.results[i].isFinal){
                    finalTranscript += transcript;
                }else{
                    interimTranscript = transcript;
                }
        }
        this.recordMessage = finalTranscript + " " + interimTranscript;
    }
        },
        stopRecord: function(){
            recognition.stop();
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
        border-top: solid gray 0.5px;
        border-bottom: solid gray 0.5px;
        padding: 8px;
        min-height: 320px;
    }
    .send-to{
        padding-top: 8px;
        padding-left: 8px;
    }
    .send-from{
        padding-bottom: 8px;
        padding-right: 32px;
        text-align: right;
    }
</style>
