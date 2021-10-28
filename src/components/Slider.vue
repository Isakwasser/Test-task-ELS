<template>
  <div class="bigContainer">
    <div class="container py-5">
      <div class="row py-3">
        <div id="sliderContainer" class="sliderItems d-flex flex-nowrap">
          <div
            class="item col-5 col-md-3 overflow-hidden position-relative"
            v-for="(el, i) in items"
            :class="el.class"
            :style="i == 0 && { marginLeft: marginLeft }"
            :key="i"
          >
            <div class="item__title">
              {{ el.title | numeric(el.isNumeric) }}
            </div>
            <div class="item__subtitle py-1" v-html="el.subtitle"></div>
            <div class="item__bg position-absolute">
              <i class="fas" :class="el.bgSrc"></i>
            </div>
          </div>
        </div>
      </div>

      <app-sliderButtons
        :numOfSlides="numOfSliders"
        :activeSlide="currentSliderPosition"
        :changeSlide="changeSlide"
      ></app-sliderButtons>
    </div>
  </div>
</template>

<script scoped>
import SliderButtons from "./SlidersButton.vue";

export default {
  data() {
    return {
      items: [
        {
          title: 15000,
          subtitle: "точек продаж",
          isNumeric: true,
          class: "item-place",
          bgSrc: "fa-map-marker-alt",
        },
        {
          title: 8,
          subtitle: "стран присутствия<br/>сервиса",
          isNumeric: true,
          class: "item-countries",
          bgSrc: "fa-globe-europe",
        },
        {
          title: 4500000,
          subtitle: "консультаций",
          isNumeric: true,
          class: "item-consult",
          bgSrc: "fa-headphones",
        },
        {
          title: 3000000,
          subtitle: "пользователей",
          isNumeric: true,
          class: "item-users",
          bgSrc: "fa-user",
        },
        {
          title: 150,
          subtitle: "корпоративных<br>партнеров",
          isNumeric: true,
          class: "item-partners",
          bgSrc: "fa-male",
        },
        {
          title: 2007,
          subtitle: "год основания",
          isNumeric: false,
          class: "item-year",
          bgSrc: "fa-city",
        },
      ],
      numOfSliders: 4,
      currentSliderPosition: 0,
      scale: 10,
      wasMounted: false,
      timer: "",
      timeToChange: 5000,
    };
  },
  methods: {
    changeSlide(num) {
      if (num >= 0 && num < this.numOfSliders) {
        this.currentSliderPosition = num;
      }
      clearInterval(this.timer);
      this.timer = setTimeout(this.moveSlides, this.timeToChange);
    },
    moveSlides() {
      this.changeSlide(
        this.currentSliderPosition + 1 == this.numOfSliders
          ? 0
          : this.currentSliderPosition + 1
      );
    },
  },
  computed: {
    marginLeft() {
      if (this.wasMounted) {
        let scale =
          (document.querySelector(".item").offsetWidth * this.items.length +
            30 * (this.items.length - 1) -
            document.getElementById("sliderContainer").offsetWidth) /
          (this.numOfSliders - 1);
        return -this.currentSliderPosition * scale + "px";
      } else {
        return -this.currentSliderPosition * this.scale + "px";
      }
    },
  },
  filters: {
    numeric(value, isNumeric) {
      if (typeof value != "number" || !isNumeric) {
        return value;
      } else {
        let str = value + "";
        let ans = "";

        while (str.length > 3) {
          ans = str.slice(str.length - 3) + " " + ans;
          str = str.slice(0, str.length - 3);
        }
        ans = str + " " + ans;
        return ans;
      }
    },
  },
  components: {
    "app-sliderButtons": SliderButtons,
  },
  mounted() {
    this.scale =
      (300 * this.items.length +
        30 * (this.items.length - 1) -
        document.getElementById("sliderContainer").offsetWidth) /
      (this.numOfSliders - 1);
    this.wasMounted = true;
    this.timer = setTimeout(this.moveSlides, 10000);
  },
};
</script>

<style scoped>
.bigContainer {
  overflow: hidden;
}
.sliderItems {
  min-height: 130px;
}
.item {
  padding: 24px;
  background-color: var(--light-color);
  color: var(--color1);
  transition: all 0.3s;
  font-size: 20px;
  position: relative;
}
.item:hover {
  box-shadow: 0 20px 30px var(--color1);
  transform: translateY(-15px);
  animation: itemGoing 2s infinite;
}

@keyframes itemGoing {
  from {
    transform: translateY(-15px);
  }
  25% {
    transform: translateY(-10px);
  }
  50% {
    transform: translateY(-15px);
  }
  75% {
    transform: translateY(-10px);
  }
  to {
    transform: translateY(-15px);
  }
}

@media (max-width: 600px) {
  .sliderItems {
    min-height: 80px;
  }
  .item {
    font-size: 10px;
  }
}

.item + .item {
  margin-left: 30px;
}
.item__title {
  font-family: "Arial";
  font-weight: bold;
  font-size: 1.8em;
  line-height: 1.4em;
  white-space: nowrap;
  text-emphasis: ellipsis;
  position: relative;
  z-index: 2;
}
.item__subtitle {
  position: relative;
  z-index: 2;

  font-size: 1em;
  line-height: 1.2em;
}
.item__bg {
  font-size: 140px;
  top: 50%;
  right: 0;
  transform: translate(20%, -53%);
  color: var(--white-bg);
  z-index: 1;
}
</style>
