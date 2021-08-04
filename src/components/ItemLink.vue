<template>
  <li>
    <a :href="`${urlLink}`" target="_blank">{{ textUrl }}</a>
  </li>
</template>

<script>
export default {
  props: {
    textUrl: {
      type: String,
    },
    urlLink: {
      type: String,
    },
  },
};
</script>

<style>
</style>