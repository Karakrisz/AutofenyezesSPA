<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const currentSlide = ref(0)
const autoPlayInterval = ref(null)

const slides = [
  {
    image: '/img/work-gallery.webp',
    alt: 'Profi autófényezés eredménye - tartós, szép munka',
    label: 'ELÉGEDETT ÜGYFELEK',
    title: 'NEM FOLTOS, NEM PÖTTYÖS - PRECÍZ MUNKA!',
    buttonText: 'KÉREK AJÁNLATOT',
    buttonLink: '/idopontfoglalas',
  },
  {
    image: '/img/work-gallery.webp',
    alt: 'Gyári minőségű autófényezés - korrekt áron',
    label: 'VÉLEMÉNYEK',
    title: 'ÜGYFELEINK AJÁNLANAK MINKET',
    buttonText: 'ÉRDEKEL A SZOLGÁLTATÁS',
    buttonLink: '/idopontfoglalas',
  },
  {
    image: '/img/work-gallery.webp',
    alt: 'Garantált minőségű fényezés - 4 napos átadás',
    label: 'GARANCIA',
    title: 'VÉGEREDMÉNYRE GARANCIÁT VÁLLALUNK',
    buttonText: 'FOGLALOM AZ IDŐPONTOT',
    buttonLink: '/idopontfoglalas',
  },
  {
    image: '/img/work-gallery.webp',
    alt: 'Minőségi alapanyagokkal készült autófényezés',
    label: 'MINŐSÉG',
    title: 'MINŐSÉGI ALAPANYAGOK - NEM SPÓROLUNK',
    buttonText: 'KÉREM A RÉSZLETEKET',
    buttonLink: '/idopontfoglalas',
  },
]

const setSlide = (index) => {
  currentSlide.value = index
}

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

onMounted(() => {
  // Start autoplay
  autoPlayInterval.value = setInterval(() => {
    nextSlide()
  }, 5000)
})

onBeforeUnmount(() => {
  // Clear interval when component is destroyed
  if (autoPlayInterval.value) {
    clearInterval(autoPlayInterval.value)
  }
})
</script>
<template>
  <!-- Hero contact bar -->
  <section class="hero">
    <div class="hero__container">
      <div class="hero__content">
        <h1 class="hero__title">
          PRECÍZ MUNKA, SZÉP EREDMÉNY<br />KORREKT ÁRON
        </h1>
      </div>

      <div class="hero__image-container position-relative">
        <div class="hero__cta position-absolute">
          <NuxtLink to="/idopontfoglalas" class="hero__cta-button"
            >INGYENES AJÁNLAT KÉRÉS</NuxtLink
          >
        </div>
        <NuxtImg
          src="/img/hero.webp"
          alt="Profi autófényezés - gyári minőségű eredmény"
          class="hero__image"
        />
      </div>
    </div>
  </section>
  <!-- Top contact bar -->
  <div class="contact-bar">
    <div class="contact-bar__container">
      <div class="contact-bar__item">
        <span class="contact-bar__icon contact-bar__icon--phone"></span>
        <a href="tel:+36703633217" class="contact-bar__link"
          >+36 (70) 363 3217</a
        >
      </div>
      <div class="contact-bar__item">
        <span class="contact-bar__icon contact-bar__icon--phone2"></span>
        <a href="tel:+3613496679" class="contact-bar__link">+36 (1) 349 6679</a>
      </div>
      <div class="contact-bar__item">
        <span class="contact-bar__icon contact-bar__icon--mail"></span>
        <a href="mailto:szerviz@autofenyezes.com" class="contact-bar__link"
          >szerviz@autofenyezes.com</a
        >
      </div>
      <div class="contact-bar__item">
        <span class="contact-bar__icon contact-bar__icon--time"></span>
        <span class="contact-bar__text"
          >H-Cs - 7:00 - 17:00 | P - 7:00 - 15:00</span
        >
      </div>
    </div>
  </div>

  <section class="paint-benefits" id="rolunk">
    <div class="paint-benefits__container container">
      <div class="paint-benefits__media">
        <NuxtImg
          src="/img/paint-benefits.webp"
          alt="Minőségi autófényezés - tartós védelem"
          class="paint-benefits__image"
          height="100%"
        />
      </div>
      <div class="paint-benefits__content">
        <h2 class="paint-benefits__title">
          MIÉRT VÁLASSZON MINKET? – PROFI MUNKAVÉGZÉS, MEGBÍZHATÓ EREDMÉNY
        </h2>
        <p class="paint-benefits__description">
          A meghúzások, karcolások, kőfelverődések és kisebb koccanások gyakoriak. 
          De nem mindegy, hogy kinek bízza az autója javítását! Nálunk precíz munka, 
          gyári színvonalú fényezés és korrekt árak várják.
        </p>
        <ul class="paint-benefits__list">
          <li class="paint-benefits__item">
            <strong class="paint-benefits__item-title"
              >Gyors szolgáltatás, 4 napos átadás</strong
            >
            – Tudjuk, milyen nehéz megoldani a mindennapokat autó nélkül. 
            Ezért garantáljuk a gyors, hatékony munkavégzést.
          </li>
          <li class="paint-benefits__item">
            <strong class="paint-benefits__item-title"
              >Minőségi alapanyagok - nem spórolunk</strong
            >
            – Az olcsó fényezésnél később lepattog a lakk, felreped a gitt. 
            Mi csak minőségi anyagokkal dolgozunk a tartós eredményért.
          </li>
          <li class="paint-benefits__item">
            <strong class="paint-benefits__item-title"
              >Végeredményre garanciát vállalunk</strong
            >
            – Nem lehet egymásra mutogatni. A kész munkára teljes garanciát 
            adunk, mert bízunk szakértelmünkben.
          </li>
        </ul>
        <p class="paint-benefits__cta-text">
          Ne kockáztasson olcsó fényezéssel! Kérjen ingyenes ajánlatot 
          kötelezettségek nélkül!
        </p>
        <NuxtLink to="/idopontfoglalas" class="paint-benefits__cta-button"
          >INGYENES AJÁNLAT KÉRÉS</NuxtLink
        >
      </div>
    </div>
    <div class="paint-benefits__container paint-benefits__container--format">
      <div class="paint-benefits__content paint-benefits__content--format">
        <h2 class="paint-benefits__title">
          Mit jelent az olcsó autófényezés? Miért kerülje el?
        </h2>
        <p class="paint-benefits__description">
          Sokakat foglalkoztat: az olcsóbb vagy drágább opció jobb választás? 
          A válasz egyértelmű. Az olcsó autófényezés gyakran jelenti: olcsó 
          alapanyagok használatát, kimaradt előkészítési lépéseket, gyorsított 
          munkavégzést. Ennek eredménye: felhős, foltos, pöttyös fényezés, 
          amely nem tapad megfelelően.
        </p>
        <p class="paint-benefits__description">
          Az igazság: ha nincs szerencséje, pár hónap múlva újra szóba kerül 
          az autófényezés. Érdemes a vásárlói visszajelzések alapján dönteni, 
          nem csak az ár alapján. A szakember kiválasztásakor az ügyfelek 
          véleményeit néze meg - ez mutatja meg a valós minőséget.
        </p>
        <p class="paint-benefits__description">
          Nálunk nem spórolunk az Ön kárára. Minden elem fényezését garantált 
          minőségben végezzük el, szakmai tapasztalat és precizitás alapján. 
          Bízza ránk nyugodtan autója javítását!
        </p>
      </div>
      <div class="paint-benefits__media">
        <NuxtImg
          src="/img/paint-benefits2.webp"
          alt="Szakszerű autófényezés folyamata"
          class="paint-benefits__image paint-benefits__image--format"
          height="100%"
        />
      </div>
    </div>
  </section>

  <section class="painting-process">
    <div class="painting-process__container">
      <h2 class="painting-process__title">MIÉRT NEM LESZ FOLTOS, PÖTTYÖS A FÉNYEZÉS NÁLUNK?</h2>

      <p class="painting-process__description">
        Sokan kérdezik: mi a különbség a drága és olcsó fényezés között? 
        A válasz a precíz munkavégzésben és a szakmai tapasztalatban rejlik. 
        Nálunk minden lépést betartunk - ezért garantálunk tartós, egyenletes, 
        gyári minőségű eredményt.
      </p>

      <div class="painting-process__steps">
        <div class="painting-process__step">
          <div class="painting-process__step-number">1</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Alapos előkészítés - nem hagyunk ki lépéseket</h3>
            <p class="painting-process__step-description">
              Az olcsó fényezésnél gyakran kimaradnak előkészítési lépések. 
              Nálunk minden sérülést, karcolást szakszerűen javítunk, alaposan 
              megtisztítjuk a felületet. Csak így lehet tartós a tapadás.
            </p>
          </div>
        </div>

        <div class="painting-process__step">
          <div class="painting-process__step-number">2</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Minőségi alapanyagok - nem spórolunk</h3>
            <p class="painting-process__step-description">
              Speciális alapozóréteget használunk, amely megerősíti a tapadást. 
              Az olcsó alapanyagok használata később problémákhoz vezet - 
              ezért mi csak minőségi termékekkel dolgozunk.
            </p>
          </div>
        </div>

        <div class="painting-process__step">
          <div class="painting-process__step-number">3</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Gyári színkód szerinti precíz festés</h3>
            <p class="painting-process__step-description">
              Pormentes fényezőkamrában, több rétegben visszük fel a festéket. 
              Nem gyorsítjuk a munkát - minden rétegnek idő kell a megfelelő 
              száradáshoz és tapadáshoz.
            </p>
          </div>
        </div>

        <div class="painting-process__step">
          <div class="painting-process__step-number">4</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Védőlakk - tartósság garantálva</h3>
            <p class="painting-process__step-description">
              UV-álló védőlakkot viszünk fel, amely megvédi a fényezést. 
              Ez biztosítja, hogy a festék ne fakúljon, ne repedezzen - 
              hosszú évekig megőrzi szépségét.
            </p>
          </div>
        </div>

        <div class="painting-process__step painting-process__step--border-0">
          <div class="painting-process__step-number">5</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">
              Polírozás és minőségellenőrzés
            </h3>
            <p class="painting-process__step-description">
              Alapos ellenőrzés után adjuk át az autót. Minden munkánkra 
              garanciát vállalunk - ha nem elégedett, javítjuk. 
              Nálunk nem lehet egymásra mutogatni.
            </p>
          </div>
        </div>
      </div>
      <div class="text-center">
        <NuxtLink to="/idopontfoglalas" class="paint-benefits__cta-button">IDŐPONTFOGLALÁS</NuxtLink>
      </div>
    </div>
  </section>
  
  <section class="work-gallery" id="galeria">
    <div class="work-gallery__container">
      <div class="work-gallery__slider">
        <div
          v-for="(slide, index) in slides"
          :key="index"
          class="work-gallery__slide"
          :class="{ 'work-gallery__slide--active': currentSlide === index }"
        >
          <div class="work-gallery__image-wrapper">
            <img
              :src="slide.image"
              :alt="slide.alt"
              class="work-gallery__image"
            />
            <div class="work-gallery__overlay">
              <span class="work-gallery__label">{{ slide.label }}</span>
              <h2 class="work-gallery__title">{{ slide.title }}</h2>
              <NuxtLink :to="slide.buttonLink" class="work-gallery__button">
                {{ slide.buttonText }}
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>

      <div class="work-gallery__nav">
        <button
          v-for="(_, index) in slides"
          :key="index"
          class="work-gallery__nav-dot"
          :class="{ 'work-gallery__nav-dot--active': currentSlide === index }"
          :aria-label="`${index + 1}. kép megjelenítése`"
          @click="setSlide(index)"
        ></button>
      </div>
    </div>
  </section>
</template>
