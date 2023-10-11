<template>
  <article class="terminal">
    <div class="container">
      <div class="terminal__console">
        <p class="terminal__console--text">
          Copyright (C) Wojciech Borys. All rights reserved.
        </p>
        <p id="text" class="terminal__console--text">
          > : Ask me a question, type something inside the console, then click
          ENTER
        </p>
        <AppTerminalRow></AppTerminalRow>
      </div>
    </div>
  </article>
</template>

<script>
import AppTerminalRow from "./AppTerminalRow.vue";

export default {
  name: "AppTerminal",

  components: {
    AppTerminalRow,
  },

  methods: {
    isInViewport: function (elem) {
      var bounding = document.querySelector(elem).getBoundingClientRect();
      return (
        bounding.top >= 0 &&
        bounding.left >= 0 &&
        bounding.bottom <=
          (window.innerHeight || document.documentElement.clientHeight) &&
        bounding.right <=
          (window.innerWidth || document.documentElement.clientWidth)
      );
    },
  },

  mounted() {},
};
</script>

<style lang="scss"></style>
