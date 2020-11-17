<template>
  <div class="trafficLights_red">
    <div class="redLight">
      <Timer :workTime="workTime" />
    </div>
    <div class="yellowLight"></div>
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
      workTime: time === "0" || +time > 10 || !time ? 10 : time,
    };
  },
  mounted() {
    this.changeLight();
  },
  methods: {
    changeLight: function () {
      this.$root.$refs.light.changeLight(".redLight", "yellow");
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../scss/mixins";

.trafficLights_red {
  @include trafficLight;

  .redLight {
    @include light(red, 1);
  }

  .yellowLight {
    @include light(yellow, 0.3);
  }

  .greenLight {
    @include light(green, 0.3);
  }
}
</style>