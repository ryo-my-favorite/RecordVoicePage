<template>
  <v-app>
    <v-toolbar app class="brown lighten-3">
      <v-toolbar-title class="headline ">
        <span>LaLaLa Contest <span style="font-size:16px;">〜たくさん「ら」と言うゲーム〜</span></span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat
        href="https://developers.google.com/web/updates/2013/01/Voice-Driven-Web-Apps-Introduction-to-the-Web-Speech-API"
        target="_blank"
      >
        <span class="mr-2">Speech Recognition</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <TopPage/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import TopPage from './components/TopPage'

export default {
  name: 'App',
  components: {
    TopPage
  },
  data () {
    return {
      //
    }
  }
}
</script>
