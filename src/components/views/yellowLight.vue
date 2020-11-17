<template>
  <div class="trafficLights_yellow">
    <div class="redLight"></div>
    <div class="yellowLight">
      <Timer :workTime="workTime" />
    </div>
    <div class="greenLight"></div>
  </div>
</template>

<script>
import Timer from "@/components/timer.vue";

export default {
  components: {
    Timer,
  },
  data() {
    const time = localStorage.getItem("time");
    return {
      nextPath: "",
      workTime: time === "0" || +time > 3 || !time ? 3 : time,
    };
  },
  beforeRouteEnter(to, from, next) {
    next((vm) => {
      if (from.path == "/red") {
        vm.nextPath = "/green";
      } else {
        vm.nextPath = "/red";
      }
      vm.changeLight(".yellowLight", vm.nextPath);
    });
  },
  mounted() {},

  methods: {
    changeLight: function (className, route) {
      this.$root.$refs.light.changeLight(className, route);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../scss/mixins";

.trafficLights_yellow {
  @include trafficLight;

  .yellowLight {
    @include light(yellow, 1);
  }

  .redLight {
    @include light(red, 0.3);
  }

  .greenLight {
    @include light(green, 0.3);
  }
}
</style>