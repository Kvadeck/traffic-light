<template>
  <div class="trafficLights_green">
    <div class="redLight"></div>
    <div class="yellowLight"></div>
    <div class="greenLight">
      <Timer :workTime="workTime" />
    </div>
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
      workTime: time === "0" || !time ? 15 : time,
    };
  },
  mounted() {
    this.changeLight();
  },
  methods: {
    changeLight: function () {
      this.$root.$refs.light.changeLight(".greenLight", "yellow");
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../scss/mixins";

.trafficLights_green {
  @include trafficLight;

  .greenLight {
    @include light(green, 1);
  }

  .redLight {
    @include light(red, 0.3);
  }

  .yellowLight {
    @include light(yellow, 0.3);
  }
}
</style>