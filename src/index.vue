<script>
import { defineComponent } from "vue";
import DarkReader from "@/DarkReader.vue";

export default defineComponent({
  name: "ServeDev",
  components: {
    DarkReader,
  },
  data() {
    return {
      isDarkMode: false,
    };
  },
  methods: {
    toggleDarkMode() {
      this.isDarkMode = this.isDarkMode ? false : true;
    },
  },
});
</script>

<template>
  <div id="app">
    <DarkReader :dark="isDarkMode" />
    <button @click="toggleDarkMode">Toggle</button>
  </div>
</template>
