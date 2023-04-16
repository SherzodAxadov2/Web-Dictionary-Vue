<script setup>
import { ref } from "vue";
import HeaderSelectors from "../home-header/HeaderSelectors.vue";

let isSelectorActive = ref(false);
const headerSelectors = ref([
  { id: 1, title: "Sans Serif" },
  { id: 2, title: "Serif" },
  { id: 3, title: "Mono" },
]);

// const showSelect = function () {
//   isSelectorActive = ref(!isSelectorActive._value);
//   console.log(isSelectorActive);
// };
</script>
<template>
  <header class="header">
    <div class="container">
      <div class="header__wrapper">
        <div class="header__logo">
          <router-link to="/">
            <img src="@/assets/images/logo.png" alt="logo" />
          </router-link>
        </div>

        <div class="header__widgets">
          <div class="header__select" @click="!isSelectorActive._value">
            <p class="header__select--selected body-m text-black-2d">Sans Serif</p>
            <img src="@/assets/icons/select-icon.png" alt="icon" />
            <div class="header__selectors" v-show="isSelectorActive._value">
              <ul>
                <HeaderSelectors
                  v-for="{ title, id } in headerSelectors"
                  :key="id"
                  :selector="title"
                />
              </ul>
            </div>
          </div>
          <span></span>
          <div class="header__toggle">
            <div class="header__toggle__btn" onclick="darkMode()"><span></span></div>
            <i class="fa-solid fa-moon" onclick="darkMode()"></i>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>
<style lang=""></style>
