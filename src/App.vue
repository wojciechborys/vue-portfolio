<template>
  <div id="app" :class="{ dark: darkMode === true }">
    <AppHeader @clicked="checkModeState"></AppHeader>
    <AppHero></AppHero>
    <AppTerminal></AppTerminal>
    <AppContact></AppContact>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppHero from "./components/AppHero.vue";
import AppTerminal from "./components/AppTerminal.vue";
import AppContact from "./components/AppContact.vue";
import ScrollMagic from "scrollmagic";

export default {
  name: "App",
  components: {
    AppHero,
    AppTerminal,
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

        stars.push({ style: starStyle, index: index }); // Dodaj indeks
      }
      this.stars = stars;
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
</style>
