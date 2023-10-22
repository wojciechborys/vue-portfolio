<template>
  <div id="app" ref="mainbody" :class="{ dark: darkMode }">
    <AppHeader @clicked="changeState" @scrollTo="scrollTo"></AppHeader>
    <AppHero :stars="stars" @scrollTo="scrollTo"></AppHero>
    <AppTerminal></AppTerminal>
    <AppFooter :darkMode="darkMode"></AppFooter>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppHero from "./components/AppHero.vue";
import AppTerminal from "./components/AppTerminal.vue";
import AppFooter from "./components/AppFooter.vue";
import ScrollMagic from "scrollmagic";

export default {
  name: "App",
  components: {
    AppHero,
    AppTerminal,
    AppHeader,
    AppFooter,
  },
  data() {
    return {
      stars: [],
      popupState: false,
      darkMode: false,
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

    modeState() {
      const storedValue = localStorage.getItem("state");
      let val = storedValue === "true";
      if (localStorage.getItem("state")) {
        this.darkMode = val;
      }
      this.changeBckgColor();
      console.log("APP Main" + this.darkMode);
    },

    changeBodyClass() {
      this.$refs.mainbody.classList.toggle("dark");
    },

    changeState() {
      this.changeBodyClass();
      this.modeState();
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
      let appElement = document.querySelector("#app");
      let darkStartColor = [15, 15, 15];
      let darkEndColor = [95, 104, 119];
      let lightStartColor = [240, 240, 240];
      let lightEndColor = [179, 179, 179];
      if (this.darkMode) {
        appElement.style.backgroundColor = `rgb(${darkStartColor})`;
      } else {
        appElement.style.backgroundColor = `rgb(${lightStartColor})`;
      }

      new ScrollMagic.Scene({
        duration: 500,
        offset: 100,
      })
        .on("progress", (event) => {
          let progress = event.progress;

          let transitionColor = [];

          if (this.darkMode) {
            transitionColor = darkStartColor.map((channel, index) => {
              let difference = darkEndColor[index] - channel;
              let transitionValue = channel + difference * progress;
              return Math.round(transitionValue);
            });
          } else {
            transitionColor = lightStartColor.map((channel, index) => {
              let difference = lightEndColor[index] - channel;
              let transitionValue = channel + difference * progress;
              return Math.round(transitionValue);
            });
          }

          appElement.style.backgroundColor = `rgb(${transitionColor.join(
            ","
          )})`;
        })
        .addTo(controller);
    },
  },

  mounted() {
    this.modeState();
    this.initializeStars();
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/main.scss";
</style>
