<script setup>
const links = [
  { name: 'Főoldal', path: '/', noBorder: false },
  { name: 'GALÉRIA', path: '/', noBorder: false },
  { name: 'RÓLUNK', path: '/', noBorder: false },
  { name: 'KAPCSOLAT', path: '/', noBorder: false },
  { name: 'REFERENCIÁK', path: '/', noBorder: true },
  { name: 'SZOLGÁLTATÁSOK', path: '/', noBorder: true },
]

const isMenuOpen = ref(false)
</script>

<template>
  <header class="header">
    <div class="header-content d-flex">
      <div class="logo-box header-content__logo-box">
        <a href="/" class="header-content__logo-box__link">
          <NuxtImg
            src="/img/logo.png"
            alt="Biztos Alkuszom"
            class="header-content__logo-box__link__img"
            height="100%"
          />
        </a>
      </div>
      <div class="nav-box header-content__nav-box d-flex">
        <button
          @click="isMenuOpen = !isMenuOpen"
          class="hamburger"
          :class="{ open: isMenuOpen }"
        >
          <div class="bar"></div>
          <div class="bar"></div>
          <div class="bar"></div>
        </button>
        <nav :class="{ 'menu--open': isMenuOpen, menu: true }" id="menu">
          <ul id="menu__list" class="menu__list d-flex">
            <li
              v-for="link in links"
              :key="link.path"
              class="menu__list__li"
              :class="{ 'menu__list__li--no-border': link.noBorder }"
            >
              <NuxtLink
                :to="link.path"
                :class="[
                  'menu__item text-color text-transform-uppercase',
                  { 'menu__item--no-border': link.noBorder },
                ]"
              >
                <template v-if="link.imagePath">
                  <NuxtImg
                    class="menu__list__li__img"
                    height="100%"
                    :src="link.imagePath"
                    :alt="link.name"
                  />
                </template>
                <template v-else>
                  {{ link.name }}
                </template>
              </NuxtLink>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </header>
</template>
