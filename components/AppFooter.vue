<script setup>
// Egyszerűsített script, nincs szükség az email küldésre
</script>

<template>
  <footer>
    <div class="footer-content d-flex container" id="kapcsolat">
      <div class="footer-content__map">
        <iframe
          class="footer-content__map__iframe"
          src="https://www.google.com/maps/embed?pb=!1m23!1m12!1m3!1d21525.896975087788!2d19.04182205!3d47.592355000000005!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!4m8!3e6!4m0!4m5!1s0x4741dbbcd5112291%3A0x8151ab1ec39bdcf2!2sBudapest%2C%20Tatai%20u.%2082%2C%201135!3m2!1d47.535564699999995!2d19.0913154!5e0!3m2!1shu!2shu!4v1758191051495!5m2!1shu!2shu"
          style="border: 0"
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
        ></iframe>
      </div>
      <div class="footer-content__form bg-color-w">
        <h6
          class="footer-content__form__h6 text-transform-uppercase text-center f-700 text-color"
        >
          IDŐPONTFOGLALÁS
        </h6>
        
        <div class="footer-cta-content">
          <h3 class="footer-cta-title">Kérjen ingyenes ajánlatot!</h3>
          <p class="footer-cta-text">
            Precíz munka, gyári minőségű fényezés korrekt áron. 
            4 napos átadás garantálva!
          </p>
          
          <div class="footer-cta-benefits">
            <div class="benefit-item">✓ Ingyenes árajánlat</div>
            <div class="benefit-item">✓ Gyors szolgáltatás</div>
            <div class="benefit-item">✓ Minőségi alapanyagok</div>
          </div>
          
          <div class="footer-cta-button-wrapper">
            <NuxtLink
              to="/idopontfoglalas"
              class="contact-form__link-box__text-box__btn d-flex page-link text-color-w cursor"
            >
              IDŐPONTFOGLALÁS
              <NuxtImg
                src="/img/right.svg"
                alt="Nyíl ikon"
                class="contact-form__link-box__text-box__btn__img position-relative"
                height="100%"
              />
            </NuxtLink>
          </div>
        
        </div>
      </div>
    </div>
    <div class="footer-brand-content text-center">
      <NuxtImg
        src="/img/brand.svg"
        alt="Autó fényezés"
        class="footer-brand-content__img"
        height="100%"
      />
    </div>
  </footer>
</template>