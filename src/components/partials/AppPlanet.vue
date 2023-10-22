<template>
  <div :class="type">
    <div class="ring" v-if="ring"></div>
    <div class="cover-ring" v-if="ring"></div>
    <div class="spots">
      <span v-for="(spot, index) in spots" :key="index"></span>
    </div>
  </div>
</template>
<script>
export default {
  name: "AppPlanet",
  data() {},

  props: {
    spots: {
      type: Number,
      required: false,
    },
    ring: {
      type: Boolean,
      required: false,
    },

    type: {
      type: String,
      required: true,
    },
  },
};
</script>
