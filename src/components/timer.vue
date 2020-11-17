<template>
  <div class="timer">{{ currentTime }}</div>
</template>

<script>
export default {
  data() {
    return {
      timer: null,
      interval: null,
    };
  },
  props: ["workTime"],
  mounted() {
    this.timer = this.workTime;
    this.interval = setInterval(() => {
      this.timer--;
    }, 1000);
  },
  computed: {
    currentTime() {
      if (this.timer <= 0) {
        clearInterval(this.interval);
        localStorage.removeItem("time", this.timer);
        return 0;
      }
      localStorage.setItem("time", this.timer);
      return this.timer;
    },
  },
  created() {
    this.$root.$refs.light = this;
  },
  methods: {
    changeLight: function (className, route) {
      const el = document.querySelector(className);
      let timerId = setTimeout(function opacityChange() {
        el.style.opacity = el.style.opacity === "0.3" ? "1" : "0.3";
        timerId = setTimeout(opacityChange, 700);
      }, (this.workTime - 3) * 1000);
      
      setTimeout(() => {
        clearTimeout(timerId);
        this.$router.push(route);
      }, this.workTime * 1000);
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@100;400&display=swap");

.timer {
  font-family: "Roboto", sans-serif;
  font-size: 2.2rem;
  color: white;
}
</style>