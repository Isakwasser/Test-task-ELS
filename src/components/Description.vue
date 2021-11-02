<template>
  <div class="container">
    <div class="row align-items-center align-items-lg-end">
      <h2
        class="
          my-2 my-md-5
          col-sm-7 col-md-9 col-lg-12
          order-2 order-sm-1
          align-center
        "
      >
        О компании
      </h2>
      <div
        class="
          col-sm-5 col-md-3 col-lg-4 col-xl-3
          my-2
          order-1 order-sm-2
          logo-img
        "
      >
        <img src="../assets/logo.svg" alt="" />
      </div>
      <div class="col-lg-8 col-xl-9 order-3">
        Европейская Юридическая Служба была основана в 2007 году, создав на
        рынке новую товарную категорию круглосуточной дистанционной юридической
        поддержки. Компания стала первой, предложившей рынку онлайн услугу
        юридической профилактики по всем видам права.
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>


<style scoped>
.container {
  color: var(--dark-gray);
}
h2 {
  font-weight: bold;
  font-size: 36px;
  line-height: 41px;
}
div {
  font-size: 18px;
  line-height: 22px;
}
.logo-img img {
  width: 90%;
  /* animation: logo 10s linear infinite; */
}
@keyframes logo {
  from {
    filter: hue-rotate(0deg);
  }
  10% {
    filter: hue-rotate(360deg);
  }
  to {
    filter: hue-rotate(360deg);
  }
}
</style>