<template>
  <div class="calculator__container">
    <div class="calculator__main">
      <div class="calculator__top">
        <div class="calculator__title">Калькулятор</div>
        <div class="calculator__text">
          Калькулятор доходности майнинга поможет узнать, какие альткоины
          выгодно майнить и какой доход принесет оборудование с учетом затрат на
          электроэнергию.
        </div>
      </div>
      <div class="calculator__form">
        <input
          type="text"
          class="calculator__input"
          placeholder="Ваш хэшрейт TH/s"
        />
        <div class="calculator__select_con" :class="{ open: select_is_open }">
          <div
            @click="select_is_open = !select_is_open"
            class="calculator__select_title"
          >
            {{ select_option }}
          </div>
          <div class="calculator__select_options">
            <div
              v-for="option in calculatorOptions"
              :key="option.value"
              class="calculator__select_option"
            >
              <p @click="selectOption(option.title)">{{ option.title }}</p>
            </div>
          </div>
        </div>
        <blue-button>
          <a href="#" class="all-link">Начать майнинг</a>
        </blue-button>
      </div>
    </div>
  </div>
</template>

<script>
import BlueButton from "./UI/BlueButton";
export default {
  components: {
    BlueButton,
  },
  data() {
    return {
      calculatorOptions: [
        { title: "Bitcoin", value: 1 },
        { title: "Bitcoin Cash", value: 2 },
        { title: "Litecoin", value: 3 },
        { title: "Dash", value: 4 },
      ],
      select_option: "Bitcoin",
      select_is_open: false,
    };
  },
  methods: {
    selectOption(option) {
      this.select_option = option;
    },
    hideSelect() {
      this.select_is_open = false;
    },
  },
  mounted() {
    document.addEventListener("click", this.hideSelect.bind(this), true);
  },
};
</script>

<style lang="scss" scoped>
.calculator {
  margin-top: 100px;
  // .calculator__main
  &__main {
  }
  // .calculator__top
  &__top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    @media (max-width: 1270px) {
      display: block;
    }
  }
  // .calculator__title
  &__title {
    font-family: "AmpleSoftPro";
    font-style: normal;
    font-weight: 500;
    font-size: 53px;
    line-height: 107.6%;
    color: #000034;
    @media (max-width: 1270px) {
      margin-bottom: 16px;
    }
    @media (max-width: 991.98px) {
      text-align: center;
    }
    @media (max-width: 767.98px) {
      font-size: 35px;
      line-height: 107.6%;
    }
  }
  // .calculator__text
  &__text {
    max-width: 730px;
    font-style: normal;
    font-weight: 300;
    font-size: 18px;
    line-height: 181.1%;
    color: #000000;
    @media (max-width: 767.98px) {
      font-size: 16px;
      line-height: 148.6%;
    }
  }
  // .calculator__form
  &__form {
    display: flex;
    margin-top: 40px;
    gap: 26px;
    @media (max-width: 991.98px) {
      margin-top: 26px;
      flex-direction: column;
    }
    & .blue-button {
      @media (max-width: 479.98px) {
        width: 100%;
        & a {
          font-size: 18px;
          line-height: 107.6%;
        }
      }
    }
  }
  // .calculator__input
  &__input {
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.16);
    border-radius: 10px;
    font-style: normal;
    font-weight: 300;
    font-size: 18px;
    line-height: 181.1%;
    color: rgba(0, 0, 0, 0.72);
    padding: 14px 30px;
  }
  // .calculator__select
  &__select {
    // .calculator__select_con
    &_con {
      position: relative;
      &.open {
        & .calculator__select_title {
          pointer-events: none;
          @media (min-width: 991.98px) {
            transform: scale(1.05);
          }
          &::after {
            transform: rotate(-180deg);
          }
        }
        & .calculator__select_options {
          pointer-events: all;
          opacity: 1;
          visibility: visible;
          top: 0px;
          @media (min-width: 991.98px) {
            transform: scale(1.05);
          }
        }
      }
    }
    // .calculator__select_title
    &_title {
      cursor: pointer;
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.16);
      border-radius: 10px;
      font-style: normal;
      font-weight: 400;
      font-size: 18px;
      line-height: 181.1%;
      color: #000000;
      height: 100%;
      width: 320px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 20px;
      position: relative;
      transition: all 0.3s ease 0s, pointer-events 0s;
      @media (max-width: 991.98px) {
        padding: 14px 20px;
        width: 100%;
      }
      &::after {
        content: "";
        background-image: url("../assets/img/arrow-down-icon-blue.svg");
        background-position: center;
        background-size: contain;
        background-repeat: no-repeat;
        width: 18px;
        height: 18px;
        transition: all 0.3s ease 0s;
      }
    }
    // .calculator__select_options
    &_options {
      pointer-events: none;
      position: absolute;
      z-index: 2;
      background: #ffffff;
      border: 1px solid rgba(0, 0, 0, 0.16);
      border-radius: 10px;
      width: 100%;
      overflow: hidden;
      opacity: 0;
      visibility: hidden;
      top: -10px;
      transition: all 0.3s ease 0s, pointer-events 0s 0.3s;
    }
    // .calculator__select_option
    &_option {
      cursor: pointer;
      font-style: normal;
      font-weight: 400;
      font-size: 18px;
      line-height: 181.1%;
      color: #000000;
      display: flex;
      flex-direction: column;
      & p {
        padding: 0 20px;
      }
      &:not(:last-child) {
        &::after {
          content: "";
          width: 100%;
          height: 1px;
          background: rgba(0, 0, 0, 0.09);
        }
      }
      transition: all 0.3s ease 0s;
      &:hover,
      &:active {
        color: #fff;
        background: #3f7bdd;
      }
    }
  }
}

.all-link {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
