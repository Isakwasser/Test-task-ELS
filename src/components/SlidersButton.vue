<template>
  <div class="d-flex align-items-center justify-content-center">
    <div
      class="changeBtn d-flex align-items-center justify-content-start px-2"
      @click="changeLeft"
    >
      <i class="fas fa-chevron-left"></i>
    </div>

    <div class="selectSlide d-flex mx-4">
      <div
        class="d-flex align-items-center mx-1"
        v-for="(slide, i) in new Array(numOfSlides)"
        :key="i"
      >
        <input type="radio" name="slide" id="slide_1" class="d-none" />
        <label
          for="slide_1"
          :class="activeSlide == i && 'active'"
          @click="changeSlide(i)"
        ></label>
      </div>
    </div>

    <div
      class="changeBtn d-flex align-items-center justify-content-end px-2"
      @click="changeRight"
    >
      <i class="fas fa-chevron-right"></i>
    </div>
  </div>
</template>

<script>
export default {
  props: ["changeSlide", "numOfSlides", "activeSlide"],
  data() {
    return {};
  },
  methods: {
    changeLeft() {
      let current = this.activeSlide;

      if (current > 0 && current < this.numOfSlides) {
        this.changeSlide(current - 1);
      }
    },
    changeRight() {
      let current = this.activeSlide;
      if (current >= 0 && current < this.numOfSlides - 1) {
        this.changeSlide(current + 1);
      }
    },
  },
};
</script>

<style scoped>
.changeBtn {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  color: var(--bright-color);

  border: 1px solid var(--bright-color);

  cursor: pointer;
}
.selectSlide label {
  width: 8px;
  height: 8px;

  border-radius: 50%;

  background: var(--gray-color);

  transition: all 0.4s;
  cursor: pointer;
}
label.active {
  transform: scale(1.375);
  background: var(--bright-color);
}
</style>
