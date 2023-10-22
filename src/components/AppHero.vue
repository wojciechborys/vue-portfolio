<template>
  <div class="introduction">
    <div class="container">
      <div class="introduction__content">
        <template v-if="isMobile">
          <h1>Hello, my name is Wojciech Borys</h1>
          <h2>
            I am Poland based Wordpress / Vue Developer, currently looking for
            work
          </h2></template
        >
        <template v-else>
          <h1>
            <vue-typer
              text="Hello, my name is Wojciech Borys"
              caret-animation="smooth"
              :repeat="0"
            ></vue-typer>
          </h1>
          <h2>
            <vue-typer
              :pre-type-delay="5000"
              caret-animation="smooth"
              text="I am Poland based Wordpress / Vue Developer, currently looking for work"
              :repeat="0"
            ></vue-typer>
          </h2>
        </template>
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
    </div>
  </div>
</template>

<script>
import { VueTyper } from "vue-typer";

export default {
  name: "App",
  components: {
    VueTyper,
  },
  data() {
    return {};
  },

  props: {
    stars: {
      type: Array,
      required: true,
    },
  },

  computed: {
    isMobile() {
      return window.innerWidth <= 992;
    },
  },

  methods: {
    scrollTo(el) {
      this.$emit("scrollTo", el);
    },
  },
};
</script>
