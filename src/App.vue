<template>
  <div id="app" class="show-smoothly">
    <app-description></app-description>
    <app-slider></app-slider>
    <app-form></app-form>
  </div>
</template>

<script>
import Desription from "./components/Description.vue";
import Slider from "./components/Slider.vue";
import Form from "./components/Form.vue";

export default {
  components: {
    "app-description": Desription,
    "app-slider": Slider,
    "app-form": Form,
  },
};
</script>

<style>
:root {
  --white-bg: #ffffff;
  --color1: #606991;
  --light-color: #f4f7fa;
  --bright-color: #296093;
  --gray-color: #959595;
  --dark-gray: #2f3441;
  --dark-blue-color: #1f3669;
  --label-color: #676b78;
  --error-color: #df2030;
}
html,
body {
  font-family: Arial, sans-serif;
  font-style: normal;
  min-width: 500px;
}

.show-smoothly {
  animation: show-smoothly linear 2s forwards;
}
@keyframes show-smoothly {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
