<template>
  <div class="main">
    <div class="container py-5">
      <div class="row">
        <div class="col-lg-6 text-end photo-section">
          <img src="../assets/formImage.png" alt="" />
          <p>Уже есть бизнес?<br />Откройте счет прямо сейчас!</p>
        </div>
        <div class="col-lg-6">
          <form @submit="submitForm">
            <h3 class="mb-4">
              Оставьте заявку на открытие счёта, и специалист&nbsp;банка «ВТБ»
              свяжется с Вами в самое&nbsp;ближайшее время
            </h3>
            <div class="form-floating mb-4">
              <input
                type="text"
                class="form-control"
                id="name"
                placeholder="Наименование заявителя"
                v-model="name"
                @input="isChanged"
              />
              <label for="name" class="required">Наименование заявителя</label>
              <div class="invalid-feedback position-absolute">
                Необходимо заполнить поле
              </div>
            </div>

            <div class="form-floating mb-4">
              <input
                type="text"
                class="form-control"
                id="contactPerson"
                placeholder="Контактное лицо"
                v-model="contactPerson"
                @input="isChanged"
              />
              <label for="contactPerson" class="required"
                >Контактное лицо</label
              >
              <div class="invalid-feedback position-absolute">
                Необходимо заполнить поле
              </div>
            </div>

            <div class="form-floating mb-5">
              <input
                type="tel"
                class="form-control"
                id="tel"
                placeholder="Телефон"
                v-model="tel"
                @input="isChanged"
              />
              <label for="tel" class="required">Телефон</label>
              <div class="invalid-feedback feedback">
                Просьба указать телефон с кодом города. В формате: (код города)
                номер телефона
              </div>
            </div>

            <div class="form-check p-0 d-flex align-items-start my-4">
              <input
                class="form-check-input"
                type="checkbox"
                id="isAgree"
                v-model="isAgree"
                @input="isChanged"
              />
              <label for="isAgree" class="check"
                ><i class="fas fa-check"></i
              ></label>
              <label class="form-check-label mx-3" for="isAgree">
                Оставляя заявку, вы принимаете условия Пользовательского
                соглашения и&nbsp;Политики конфиденциальности.
              </label>
            </div>

            <button type="submit" class="btn btn-danger mt-4">
              Оставить заявку
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "inputmask";

export default {
  data() {
    return {
      name: "",
      contactPerson: "",
      tel: "",
      isAgree: false,
    };
  },
  methods: {
    submitForm() {
      event.preventDefault();
      let isValid = true;
      if (!this.name) {
        isValid = false;
        document.getElementById("name").classList.remove("is-invalid");
        document.getElementById("name").offsetWidth;
        document.getElementById("name").classList.add("is-invalid");
      }
      if (!this.contactPerson) {
        isValid = false;
        document.getElementById("contactPerson").classList.remove("is-invalid");
        document.getElementById("contactPerson").offsetWidth;
        document.getElementById("contactPerson").classList.add("is-invalid");
      }
      if (!this.tel || this.tel.indexOf("_") != -1) {
        isValid = false;
        document.getElementById("tel").classList.remove("is-invalid");
        document.getElementById("tel").offsetWidth;
        document.getElementById("tel").classList.add("is-invalid");
      }
      if (!this.isAgree) {
        isValid = false;
        document.getElementById("isAgree").classList.remove("is-invalid");
        document.getElementById("isAgree").offsetWidth;
        document.getElementById("isAgree").classList.add("is-invalid");
      }
      if (isValid) {
        localStorage.setItem("app-test-name", this.name);
        localStorage.setItem("app-test-contactPerson", this.contactPerson);
        localStorage.setItem("app-test-tel", this.tel);
        alert(
          `Данные отправлены, а также сохрвнены в localStorage. Они будут показаны при перезагрузке страницы`
        );
      }
    },
    isChanged() {
      event.target.classList.remove("is-invalid");
    },
  },
  mounted() {
    var selector = document.getElementById("tel");
    var im = new Inputmask("+7(999) 999 99 99");
    im.mask(selector);

    this.name = localStorage.getItem("app-test-name");
    this.contactPerson = localStorage.getItem("app-test-contactPerson");
    this.tel = localStorage.getItem("app-test-tel");
  },
};
</script>




<style scoped>
h3 {
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: 28px;

  color: var(--dark-gray);
}

.main {
  background-color: var(--light-color);
}
input,
label {
  background: transparent;
  padding-left: 0 !important;
  border-radius: 0;

  font-family: Arial;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 18px;

  color: var(--dark-gray);
}
label {
  color: var(--label-color);
  opacity: 1 !important;
}
.required:after {
  content: "*";
  color: red;
}
.is-invalid,
.is-invalid ~ * {
  color: var(--error-color) !important;
  background-image: none;
}
.is-invalid:focus {
  box-shadow: none;
}
input {
  border: none;
  border-bottom: 1px solid var(--dark-gray);
}
input:focus {
  box-shadow: none;
  background: transparent;
  border-bottom: 1px solid var(--dark-gray);
}

.form-floating > .form-control:focus ~ label,
.form-floating > .form-control:not(:placeholder-shown) ~ label,
.form-floating > .form-select ~ label {
  transform: scale(0.85) translateY(-0.7rem) translateX(-0.1rem);
}

.feedback {
  display: block;
  color: #333333;

  font-size: 12px;
  line-height: 14px;
}
.is-invalid ~ .feedback {
  color: var(--error-color);
}
input[type="checkbox"] {
  display: none;
}
input[type="checkbox"] ~ .check {
  border: 1px solid var(--dark-gray);
  border-radius: 0;
  position: relative;
  width: 17px;
  height: 17px;
  font-size: 17px;
  color: #002882;
}
input[type="checkbox"]:not(:checked) ~ .check i {
  display: none;
}
input[type="checkbox"] ~ label {
  font-size: 12px;
  line-height: 14px;
  color: var(--dark-gray);
  max-width: 430px;
}
button {
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 18px;

  color: var(--white-bg);
  height: 60px;
  width: 182px;
  background-color: var(--error-color);
  border: none;
  transition: all 0.1s;
  box-shadow: none !important;
}
button:hover {
  background-color: #ca1920;
}
button:active {
  background-color: #ca1920;
  box-shadow: inset 0px 4px 4px rgba(0, 0, 0, 0.25) !important;
}

.is-invalid {
  /* animation: error 0.5s; */
}

@keyframes error {
  from {
    transform: translateX(0px);
  }
  20% {
    transform: translateX(-5x);
  }
  40% {
    transform: translateX(5px) scale(1.1) rotate(1deg);
  }
  60% {
    transform: translateX(-5px) scale(1.1) rotate(-1deg);
  }
  80% {
    transform: translateX(5px);
  }
  to {
    transform: translateX(0px);
  }
}
.photo-section {
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 21px;

  color: var(--dark-gray);
}
.photo-section img {
  width: 100%;
}
.photo-section p {
  margin-right: 50px;
}
</style>