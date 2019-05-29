<template>
    <v-app>
        <h1>Microphone Test</h1>   
        <div>
            <v-btn small v-on:click="startRecord">Start Record</v-btn>
            <v-btn small v-on:click="stopRecord">Stop Record</v-btn>
        </div>
        <div>
            <span>{{ recordMessage }}</span>
        </div>
    </v-app>
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
            recordMessage: 'here is'
        }
    },
    methods: {
        startRecord: function(){
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

</style>
