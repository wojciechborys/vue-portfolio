<template>
  <footer class="leave-a-msg">
    <div class="container">
      <div class="leave-a-msg__wrapper">
        <div class="leave-a-msg__text">
          <h2 class="leave-a-msg__header">Hey! Don't go yet!</h2>
          <p class="leave-a-msg__text">
            Didn't find enough information? <strong>Ask me anything!</strong>
          </p>
          <a class="leave-a-msg__mail" href="mailto:hello@creavity.pl"
            >hello@creavity.pl</a
          >
        </div>
        <div class="leave-a-msg__planets">
          <div class="planet-wrapper-one" v-show="darkMode">
            <AppPlanet :spots="7" :type="'planet'" :ring="true"></AppPlanet>
          </div>

          <div class="planet-wrapper-two" v-show="darkMode">
            <AppPlanet
              :spots="3"
              :type="'small-planet'"
              :ring="false"
            ></AppPlanet>
          </div>

          <div class="planet-wrapper-three" v-show="!darkMode">
            <AppPlanet :spots="0" :type="'sun'" :ring="false"></AppPlanet>
          </div>
        </div>
      </div>
      <aside class="leave-a-msg__socials">
        <h3>You can also find me on</h3>
        <a
          class="leave-a-msg__socials--linkedin leave-a-msg__socials--icon"
          target="_blank"
          href="https://www.linkedin.com/in/wojciech-borys-261b73190/"
          ><img src="@/assets/icons/linkedin.png"
        /></a>
        <a
          class="leave-a-msg__socials--github leave-a-msg__socials--icon"
          target="_blank"
          href="https://github.com/wojciechborys"
          ><img src="@/assets/icons/github.png"
        /></a>
      </aside>
    </div>

    <svg
      class="leave-a-msg__shape"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 1440 320"
      preserveAspectRatio="none"
    >
      <path
        fill="#0099ff"
        fill-opacity="1"
        d="M0,224L60,218.7C120,213,240,203,360,176C480,149,600,107,720,106.7C840,107,960,149,1080,154.7C1200,160,1320,128,1380,112L1440,96L1440,320L1380,320C1320,320,1200,320,1080,320C960,320,840,320,720,320C600,320,480,320,360,320C240,320,120,320,60,320L0,320Z"
      ></path>
    </svg>
  </footer>
</template>

<script>
import AppPlanet from "./partials/AppPlanet.vue";

export default {
  name: "AppFooter",
  components: {
    AppPlanet,
  },
  props: {
    darkMode: {
      type: Boolean,
      reqired: false,
    },
  },
};
</script>
