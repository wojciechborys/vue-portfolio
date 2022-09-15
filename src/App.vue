<template>
  <div id="app" :class="{'dark': darkMode === true}" >
    <div class="container">
        <ModeSwitcher @clicked="checkModeState"></ModeSwitcher>
        <div class="introduction">
            <h1><vue-typer text='Hello, my name is Wojtek' caret-animation='smooth' :repeat='0'></vue-typer></h1>
            <h2><vue-typer pre-type-delay='5000' caret-animation='smooth' text='I am Poland based Wordpress + Vue Developer, currently working @Webcrafters' :repeat='0'></vue-typer></h2>  
            <p><small data-console-trigger @click="scrollTo('.terminal')" class="green">Go on, ask me something!</small></p>
        </div>

        <AppTerminal></AppTerminal>
      </div> 
  </div>
</template>

<script>
import AppTerminal from './components/AppTerminal.vue';
import ModeSwitcher from './components/ModeSwitcher.vue';
import { VueTyper } from 'vue-typer'

export default {
  name: 'App',
  data() { 
    return {
     popupState: false,
     darkMode: localStorage.getItem('state'),
    }
  },

  methods: {
    showPopup() {
      this.popupState = true;
    },

    scrollTo(el) {
      const element = document.querySelector(el);
      element.scrollIntoView({ behavior: 'smooth'});
    },

    checkModeState(value) {
       value === true ? this.darkMode = true : this.darkMode = false;
    }
  },

  computed: {
   
  },

  components: {
    AppTerminal,
    VueTyper,
    ModeSwitcher
  }
}
</script>

<style lang="scss">
  @import "./scss/main.scss";
</style>
