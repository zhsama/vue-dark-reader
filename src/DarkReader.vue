<template>
  <div class="vue-apply-darkmode-root">
    <slot></slot>
  </div>
</template>

<script>
import { disable, enable } from "darkreader";

export default {
  props: {
    dark: { type: Boolean, default: false },
    watchSystem: { type: Boolean, default: false },
    brightness: { type: Number, default: 100 },
    contrast: { type: Number, default: 90 },
    sepia: { type: Number, default: 10 },
  },
  data() {
    return {
      systemDark: false,
      mq: null,
    };
  },
  computed: {
    appearanceSettings() {
      return (
        String(this.brightness).padStart(3, 0) +
        String(this.contrast).padStart(3, 0) +
        String(this.sepia).padStart(3, 0)
      );
    },
  },
  watch: {
    dark() {
      this.toggleDarkMode();
    },
    systemDark() {
      this.toggleDarkMode();
    },
    appearanceSettings() {
      this.toggleDarkMode();
    },
  },
  mounted() {
    if (this.mq === null && window?.matchMedia) {
      this.mq = window.matchMedia("(prefers-color-scheme: dark)");
      this.mq.addEventListener("change", this.updateSystemTheme);
    }
    this.toggleDarkMode();
  },
  beforeUnmount() {
    if (this.mq !== null) {
      this.mq.removeEventListener("change", this.updateSystemTheme);
    }
  },
  methods: {
    updateSystemTheme(update) {
      this.systemDark = update.matches;
    },
    toggleDarkMode() {
      if (window) {
        if (this.dark || (!this.dark && this.systemDark)) {
          enable({
            brightness: this.brightness,
            contrast: this.contrast,
            sepia: this.sepia,
          });
        } else disable();
      }
    },
  },
};
</script>
