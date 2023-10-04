<template>
  <div id="app" :class="{ dark: darkMode === true }">
    <div class="container">
      <AppHeader @clicked="checkModeState"></AppHeader>
      <div class="introduction">
        <h1>
          <vue-typer
            text="Hello, my name is Wojciech Borys"
            caret-animation="smooth"
            :repeat="0"
          ></vue-typer>
        </h1>
        <h2>
          <vue-typer
            pre-type-delay="5000"
            caret-animation="smooth"
            text="I am Poland based Wordpress / Vue Developer, currently looking for work"
            :repeat="0"
          ></vue-typer>
        </h2>
        <p>
          <small
            data-console-trigger
            @click="scrollTo('.terminal')"
            class="green"
            >Go on, ask me something!</small
          >
        </p>

        <div v-if="stars && stars.length">
          <div
            class="star"
            v-for="(star, index) in stars"
            :key="index"
            :style="star.style"
          ></div>
        </div>
      </div>

      <AppTerminal></AppTerminal>
      <AppContact></AppContact>
    </div>
  </div>
</template>

<script>
import AppTerminal from "./components/AppTerminal.vue";
import AppHeader from "./components/AppHeader.vue";
import { VueTyper } from "vue-typer";
import ScrollMagic from "scrollmagic";
import AppContact from "./components/AppContact.vue";

export default {
  name: "App",
  components: {
    AppTerminal,
    VueTyper,
    AppHeader,
    AppContact,
  },
  data() {
    return {
      stars: [],
      popupState: false,
      darkMode: localStorage.getItem("state"),
    };
  },

  methods: {
    showPopup() {
      this.popupState = true;
    },

    scrollTo(el) {
      const element = document.querySelector(el);
      element.scrollIntoView({ behavior: "smooth" });
    },

    checkModeState(value) {
      value === true ? (this.darkMode = true) : (this.darkMode = false);
    },

    getRandom(min, max) {
      return Math.random() * (max - min) + min;
    },

    initializeStars() {
      const stars = [];
      for (let index = 0; index < 50; index++) {
        const top = this.getRandom(0, 100) + "vh";
        const left = this.getRandom(0, 100) + "vw";
        const delay = this.getRandom(0, 15) + "s";

        const starStyle = {
          top: top,
          left: left,
          animationDelay: delay,
        };

        stars.push({ style: starStyle });
      }
      this.stars = stars;

      console.log(stars);
    },

    changeBckgColor() {
      var controller = new ScrollMagic.Controller();

      new ScrollMagic.Scene({
        duration: 500,
        offset: 100,
      })
        .on("progress", function (event) {
          var progress = event.progress; // Get the scroll progress value (between 0 and 1)
          var startColor = [15, 15, 15]; // RGB values for the initial color
          var endColor = [95, 104, 119]; // RGB values for the target color

          // Calculate the transition color based on the progress
          var transitionColor = startColor.map((channel, index) => {
            var difference = endColor[index] - channel;
            var transitionValue = channel + difference * progress;
            return Math.round(transitionValue);
          });

          var appElement = document.querySelector("#app");
          appElement.style.backgroundColor = `rgb(${transitionColor.join(
            ","
          )})`;
        })
        .addTo(controller);
    },
  },

  mounted() {
    this.changeBckgColor();
    this.initializeStars();
  },

  computed: {},
};
</script>

<style lang="scss">
@import "./scss/main.scss";
.star {
  position: absolute;
  width: 1px;
  height: 1px;
  background-color: white;
  border-radius: 50%;
  opacity: 0;
  animation: sparkle 4s normal forwards;
}

@keyframes sparkle {
  50% {
    opacity: 0.4;
    transform: scale(0.5);
    box-shadow: 0px 0px 10px 5px #ffffff5e;
  }
  100% {
    opacity: 0.8;
    transform: scale(1.2);
    box-shadow: 0px 0px 2px 1px white;
  }
}
</style>
