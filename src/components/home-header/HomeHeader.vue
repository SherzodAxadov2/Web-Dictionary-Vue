<script setup>
import { ref } from "vue";

let isSelectorActive = ref(false);
const selected = ref("Sans Serif");
const darkModeToggle = ref(false);

const headerSelectors = ref([
  { id: 1, title: "Sans Serif" },
  { id: 2, title: "Serif" },
  { id: 3, title: "Mono" },
]);

document.addEventListener("click", (event) => {
  if (!document.querySelector(".header__select").contains(event.target)) {
    isSelectorActive.value = false;
  }
});

const showSelect = function () {
  isSelectorActive.value = !isSelectorActive.value;
};

const saveFontToStorage = (font) => {
  localStorage.setItem("font-family", font);
};

const setFontFamily = (fontFamily) => {
  switch (fontFamily) {
    case "Sans Serif":
      document.body.classList = "font--sans-serif";
      break;

    case "Serif":
      document.body.classList = "font--serif";
      break;

    case "Mono":
      document.body.classList = "font--mono";
      break;

    default:
      document.body.classList = "font--sans-serif";
      break;
  }
};

if (localStorage.getItem("font-family")) {
  setFontFamily(localStorage.getItem("font-family"));
  selected.value = localStorage.getItem("font-family");
}

const setSelectorValue = (e) => {
  selected.value = e.target.textContent;
  saveFontToStorage(e.target.textContent);
  setFontFamily(e.target.textContent);
};

// Save dark mode
const saveThemeStorage = () => {
  if (document.body.getAttribute("data-theme")) {
    localStorage.setItem("theme", document.body.getAttribute("data-theme"));
  } else {
    localStorage.removeItem("theme");
  }
};

const darkMode = () => {
  darkModeToggle.value = !darkModeToggle.value;
  document.body.getAttribute("data-theme")
    ? document.body.removeAttribute("data-theme")
    : document.body.setAttribute("data-theme", "dark");
  saveThemeStorage();
};

if (localStorage.getItem("theme")) {
  document.body.setAttribute("data-theme", localStorage.getItem("theme"));
  darkModeToggle.value = true;
} else {
  darkModeToggle.value = false;
}
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
          <div class="header__select" @click="showSelect">
            <p class="header__select--selected body-m text-black-2d">{{ selected }}</p>
            <img src="@/assets/icons/select-icon.png" alt="icon" />
            <div class="header__selectors" v-if="isSelectorActive">
              <ul>
                <li
                  v-for="{ title, id } in headerSelectors"
                  :key="id"
                  @click="($event) => setSelectorValue($event)"
                >
                  <p class="body-m text-black-2d">{{ title }}</p>
                </li>
              </ul>
            </div>
          </div>
          <span></span>
          <div class="header__toggle">
            <div
              class="header__toggle__btn"
              :class="darkModeToggle ? 'dark' : ''"
              @click="darkMode"
            >
              <span></span>
            </div>
            <i class="fa-solid fa-moon" @click="darkMode"></i>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>
<style lang=""></style>
