<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const currentSlide = ref(0)
const autoPlayInterval = ref(null)

const slides = [
  {
    image: '/img/work-gallery.webp',
    alt: 'Fekete fényezett autó',
    label: 'GALÉRIA',
    title: 'MUNKÁINK MAGUKÉRT BESZÉLNEK!',
    buttonText: 'GALÉRIA',
    // buttonLink: '/galeria',
  },
  {
    image: '/img/work-gallery.webp',
    alt: 'Fényezés alatt álló autó',
    label: 'REFERENCIÁK',
    title: 'MINŐSÉGI MUNKA MINDEN ALKALOMMAL',
    buttonText: 'GALÉRIA',
    // buttonLink: '/galeria',
  },
  {
    image: '/img/work-gallery.webp',
    alt: 'Piros fényezett autó',
    label: 'MUNKÁINK',
    title: 'GYÁRI MINŐSÉG, ELÉGEDETT ÜGYFELEK',
    buttonText: 'GALÉRIA',
    // buttonLink: '/galeria',
  },
  {
    image: '/img/work-gallery.webp',
    alt: 'Részletes fényezési munka',
    label: 'PORTFÓLIÓ',
    title: 'PRECIZITÁS MINDEN RÉSZLETBEN',
    buttonText: 'GALÉRIA',
    // buttonLink: '/galeria',
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
        <h1 class="hero__title">AUTÓD MEGÉRDEMLI<br />A CSILLOGÁST</h1>
      </div>

      <div class="hero__image-container position-relative">
        <div class="hero__cta position-absolute">
          <a href="/ajanlatkeres" class="hero__cta-button">AJÁNLATKÉRÉS</a>
        </div>
        <img
          src="/img/hero.webp"
          alt="Csillogó kék autó fényszóró"
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

  <section class="paint-benefits">
    <div class="paint-benefits__container">
      <div class="paint-benefits__media">
        <NuxtImg
          src="/img/paint-benefits.webp"
          alt="paint-benefits__image"
          class="paint-benefits__image"
          height="100%"
        />
      </div>
      <div class="paint-benefits__content">
        <h2 class="paint-benefits__title">
          MIÉRT FONTOS AZ AUTÓFÉNYEZÉS? – NEM CSAK ESZTÉTIKA KÉRDÉSE
        </h2>
        <p class="paint-benefits__description">
          Sokan csak akkor gondolnak a fényezésre, ha egy baleset vagy karcolás
          miatt szükségessé válik. Pedig az autófényezés nem csupán esztétikai
          kérdés – az autó fényezése egyben védelmi funkciót is betölt.
        </p>
        <ul class="paint-benefits__list">
          <li class="paint-benefits__item">
            <strong class="paint-benefits__item-title"
              >Védi a karosszériát a rozsdásodástól</strong
            >
            – Ha a fényezés megsérül, a csupasz fém ki van téve az időjárás
            viszontagságainak, ami rozsdásodáshoz vezethet. Egy jó minőségű
            fényezés megakadályozza ezt.
          </li>
          <li class="paint-benefits__item">
            <strong class="paint-benefits__item-title"
              >Növeli az autó értékét</strong
            >
            – Egy ápolt, szép fényezés növeli az autó piaci értékét. Egy kopott,
            karcos jármű kevesebb figyelmet kap az eladáskor.
          </li>
          <li class="paint-benefits__item">
            <strong class="paint-benefits__item-title"
              >Megvédi az autót az UV-sugárzástól</strong
            >
            – Az UV-sugarak fakóvá, mattá és repedezett tehetik a festéket. A
            minőségi lakkréteg ezt megelőzi, így autója hosszabb ideig marad
            újszerű állapotban.
          </li>
        </ul>
        <p class="paint-benefits__cta-text">
          Ne hagyja, hogy egy sérülés elrontsa autója megjelenését vagy
          csökkentse annak értékét! Kérjen árajánlatot még ma!
        </p>
        <NuxtLink to="/" class="paint-benefits__cta-button"
          >AJÁNLATKÉRÉS</NuxtLink
        >
      </div>
    </div>
    <div class="paint-benefits__container paint-benefits__container--format">
      <div class="paint-benefits__content paint-benefits__content--format">
        <h2 class="paint-benefits__title">
          Az autófényezés titkai: Miért több ez, mint egyszerű festés?
        </h2>
        <p class="paint-benefits__description">
          Az autófényezés valódi művészet, amely messze túlmutat az egyszerű
          festési folyamaton. Kevesen tudják, hogy egy professzionális fényezés
          akár 15-20 különböző réteget is tartalmazhat, amelyek mindegyike
          speciális funkciót tölt be. A modern autófényezés során alkalmazott
          nanotechnológiás lakkok nem csupán esztétikai célt szolgálnak, hanem
          védelmet nyújtanak az UV-sugárzás, a savas eső, a madárürülék és egyéb
          környezeti hatások ellen is.
        </p>
        <p class="paint-benefits__description">
          Egy szakszerűen kivitelezett fényezés jelentősen növelheti járműve
          élettartamát és megőrizheti annak értékét. A legújabb
          kerámiabevonatokkal pedig olyan víztaszító felületet lehet
          kialakítani, amely akár 5-7 évig is megőrzi a frissen fényezett autó
          csillogását. Gondolt már arra, milyen hatással lehet autója
          megjelenése az Önről kialakult első benyomásra? Fedezze fel prémium
          fényezési szolgáltatásainkat, és tegye autóját igazán egyedivé!
        </p>
        <p class="paint-benefits__description">
          Gondolt már arra, milyen hatással lehet autója megjelenése az Önről
          kialakult első benyomásra? Fedezze fel prémium fényezési
          szolgáltatásainkat, és tegye autóját igazán egyedivé!
        </p>
      </div>
      <div class="paint-benefits__media">
        <NuxtImg
          src="/img/paint-benefits2.webp"
          alt="paint-benefits__image"
          class="paint-benefits__image paint-benefits__image--format"
          height="100%"
        />
      </div>
    </div>
  </section>

  <section class="painting-process">
    <div class="painting-process__container">
      <h2 class="painting-process__title">HOGYAN ZAJLIK A FÉNYEZÉS?</h2>

      <p class="painting-process__description">
        A tökéletes autófényezés precíz előkészítést, modern technológiát és
        szakértelmet igényel. A folyamat sokkal összetettebb annál, mint hogy
        egyszerűen ráfújjuk a festéket a felületre – minden lépésnek
        kulcsszerepe van abban, hogy a végeredmény tartós, egyenletes és gyári
        minőségű legyen.
      </p>

      <div class="painting-process__steps">
        <div class="painting-process__step">
          <div class="painting-process__step-number">1</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Felület előkészítése</h3>
            <p class="painting-process__step-description">
              Az autót alaposan megtisztítjuk, eltávolítjuk a sérült vagy
              megkopott festékréteget. A horpadásokat, karcolásokat kijavítjuk,
              hogy a felület teljesen sima legyen.
            </p>
          </div>
        </div>

        <div class="painting-process__step">
          <div class="painting-process__step-number">2</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Alapozás</h3>
            <p class="painting-process__step-description">
              Egy speciális alapozóréteget viszünk fel, amely megerősíti a
              tapadást és védi a karosszériát a korróziótól.
            </p>
          </div>
        </div>

        <div class="painting-process__step">
          <div class="painting-process__step-number">3</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Színkeverés és festés</h3>
            <p class="painting-process__step-description">
              A gyári színkód alapján precízen bekeverjük a festéket, majd
              pormentes fényezőkamrában, több rétegben visszük fel, hogy
              tökéletes, egyenletes fedést érjünk el.
            </p>
          </div>
        </div>

        <div class="painting-process__step">
          <div class="painting-process__step-number">4</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">Lakkozás és védelem</h3>
            <p class="painting-process__step-description">
              A festett felületre egy átlátszó védőlakkot viszünk fel, amely
              növeli a tartósságot, megvédi a fényezést az időjárási hatásoktól
              és az UV-sugárzástól.
            </p>
          </div>
        </div>

        <div class="painting-process__step painting-process__step--border-0">
          <div class="painting-process__step-number">5</div>
          <div class="painting-process__step-content">
            <h3 class="painting-process__step-title">
              Polírozás és végső ellenőrzés
            </h3>
            <p class="painting-process__step-description">
              Az utolsó simítások során a teljes felületet finoman átdolgozzuk,
              hogy a lakk hibátlanul sima és egyenletes legyen, majd alapos
              ellenőrzés után az autó készen áll az átadásra.
            </p>
          </div>
        </div>
      </div>
      <div class="text-center">
        <NuxtLink to="/" class="paint-benefits__cta-button"
          >AJÁNLATKÉRÉS</NuxtLink
        >
      </div>
    </div>
  </section>
  <section class="work-gallery">
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
