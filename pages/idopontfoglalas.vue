<script setup>
import { NuxtLink } from '#components'
import { ref } from 'vue'

useHead({
  title: 'Időpontfoglalás - Autófényezés',
})

// Reactive variables
const isSubmitting = ref(false)
const submitMessage = ref('')
const formData = ref({
  licensePlate: '',
  brand: '',
  model: '',
  year: '',
  service: '',
  name: '',
  email: '',
  phone: '',
})

// Form submission handler
const submitForm = async (event) => {
  event.preventDefault()

  if (isSubmitting.value) return

  isSubmitting.value = true
  submitMessage.value = ''

  try {
    const webhookUrl =
      'https://services.leadconnectorhq.com/hooks/65GU5RaMpJTj79t0Bf55/webhook-trigger/5789765a-ae70-4883-8303-d9e6654fec78'

    // Prepare data for GoHighLevel
    const payload = {
      // Contact information
      name: formData.value.name,
      email: formData.value.email,
      phone: formData.value.phone,

      // Vehicle information
      license_plate: formData.value.licensePlate,
      vehicle_brand: formData.value.brand,
      vehicle_model: formData.value.model,
      vehicle_year: formData.value.year,

      // Service information
      service_type: formData.value.service,

      // Additional metadata
      source: 'Autófényezés időpontfoglalási űrlap',
      form_type: 'auto_painting_booking',
      submission_date: new Date().toISOString(),

      // Custom fields for GoHighLevel
      custom_field_1: `${formData.value.brand} ${formData.value.model} (${formData.value.year})`,
      custom_field_2: formData.value.licensePlate,
      custom_field_3: getServiceDisplayName(formData.value.service),
    }

    const response = await fetch(webhookUrl, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(payload),
    })

    if (response.ok) {
      submitMessage.value =
        '✅ Sikeres időpontfoglalás! Nyitvatartási időben 24 órán belül felvesszük Önnel a kapcsolatot.'
      // Reset form
      formData.value = {
        licensePlate: '',
        brand: '',
        model: '',
        year: '',
        service: '',
        name: '',
        email: '',
        phone: '',
      }
    } else {
      throw new Error('Hiba történt a küldés során')
    }
  } catch (error) {
    console.error('Form submission error:', error)
    submitMessage.value =
      '❌ Hiba történt. Kérjük próbálja újra, vagy hívjon minket!'
  } finally {
    isSubmitting.value = false
  }
}

// Helper function to get service display name
const getServiceDisplayName = (serviceValue) => {
  const serviceMap = {
    'teljes-fenyezes': 'Teljes autófényezés',
    'reszleges-fenyezes': 'Részleges fényezés',
    'karosszeria-javitas': 'Karosszéria javítás + fényezés',
    'karcolasok-javitasa': 'Karcolások javítása',
    'primer-alapozas': 'Primer alapozás',
    'lakk-poliras': 'Lakk polírozás',
    'bumper-fenyezes': 'Lökhárító fényezés',
    'egyedi-szinek': 'Egyedi színek/fóliázás',
  }
  return serviceMap[serviceValue] || serviceValue
}
</script>

<template>
  <section>
    <div class="subpage">
      <div class="subpage-content">
        <!-- Fő üzenet -->
        <div class="trust-banner">
          <h2 class="page-color main-title">
            PROFESSZIONÁLIS AUTÓFÉNYEZÉS - MINŐSÉGI GARANCIA!
          </h2>
          <div class="trust-elements">
            <div class="trust-item">
              <span class="trust-icon">🎨</span>
              <strong>Tökéletes színegyezés</strong> - Gyári színkód alapú
              precíz keverés
            </div>
            <div class="trust-item">
              <span class="trust-icon">⚡</span>
              <strong>Gyors átadás</strong> - Míg mások 2 hetet, mi 3-5 nap
              alatt kész
            </div>
            <div class="trust-item">
              <span class="trust-icon">🛡️</span>
              <strong>Tartósság garancia</strong> - Nem hólyagosodik, nem pattog
              le, nem mattul
            </div>
          </div>
        </div>

        <div class="benefits-grid">
          <div class="benefit-card">
            <h3>Nincs színeltérés</h3>
            <p>
              <strong>Számítógépes színkeverés</strong> - Gyári színkódok
              alapján készülő festék, ami 100%-ban egyezik
            </p>
          </div>
          <div class="benefit-card">
            <h3>Gyors ügyintézés</h3>
            <p>
              <strong>3-5 nap alatt kész</strong> - Nem kell hetekig nélkülözni
              az autóját
            </p>
          </div>
          <div class="benefit-card">
            <h3>Tartós minőség</h3>
            <p>
              <strong>Profi alapanyagok</strong> - UV álló, időjárás álló
              festék, nem pattog le
            </p>
          </div>
        </div>

        <form class="appointment-form" @submit="submitForm">
          <!-- Jármű adatok -->
          <div class="form-section">
            <h3 class="section-title">Jármű adatok</h3>

            <div class="form-group">
              <label class="supage-content__ul__li__strong">Rendszám *</label>
              <input
                type="text"
                v-model="formData.licensePlate"
                required
                class="form-input"
                placeholder="pl. ABC-123"
                style="text-transform: uppercase"
                :disabled="isSubmitting"
              />
            </div>

            <div class="form-group">
              <label class="supage-content__ul__li__strong">Márka *</label>
              <input
                type="text"
                v-model="formData.brand"
                required
                class="form-input"
                placeholder="pl. Volkswagen, BMW, Opel"
                :disabled="isSubmitting"
              />
            </div>

            <div class="form-group">
              <label class="supage-content__ul__li__strong">Modell *</label>
              <input
                type="text"
                v-model="formData.model"
                required
                class="form-input"
                placeholder="pl. Golf, 320d, Astra"
                :disabled="isSubmitting"
              />
            </div>

            <div class="form-group">
              <label class="supage-content__ul__li__strong">Évjárat *</label>
              <input
                type="number"
                v-model="formData.year"
                required
                class="form-input"
                min="1990"
                max="2025"
                placeholder="pl. 2018"
                :disabled="isSubmitting"
              />
            </div>
          </div>

          <!-- Szolgáltatás típusa -->
          <div class="form-section">
            <h3 class="section-title">
              Milyen fényezési szolgáltatásra van szüksége?
            </h3>

            <div class="form-group">
              <label class="supage-content__ul__li__strong"
                >Szolgáltatás *</label
              >
              <select
                v-model="formData.service"
                required
                class="form-select"
                :disabled="isSubmitting"
              >
                <option value="">Válasszon szolgáltatást...</option>
                <option value="teljes-fenyezes">Teljes autófényezés</option>
                <option value="reszleges-fenyezes">Részleges fényezés</option>
                <option value="karosszeria-javitas">
                  Karosszéria javítás + fényezés
                </option>
                <option value="karcolasok-javitasa">Karcolások javítása</option>
                <option value="primer-alapozas">Primer alapozás</option>
                <option value="lakk-poliras">Lakk polírozás</option>
                <option value="bumper-fenyezes">Lökhárító fényezés</option>
                <option value="egyedi-szinek">Egyedi színek/fóliázás</option>
              </select>
            </div>
          </div>

          <!-- Személyes adatok -->
          <div class="form-section">
            <h3 class="section-title">Személyes adatok</h3>

            <div class="form-group">
              <label class="supage-content__ul__li__strong">Név *</label>
              <input
                type="text"
                v-model="formData.name"
                required
                class="form-input"
                placeholder="Teljes név"
                :disabled="isSubmitting"
              />
            </div>

            <div class="form-group">
              <label class="supage-content__ul__li__strong">Email cím *</label>
              <input
                type="email"
                v-model="formData.email"
                required
                class="form-input"
                placeholder="A megerősítést ide küldjük"
                :disabled="isSubmitting"
              />
            </div>

            <div class="form-group">
              <label class="supage-content__ul__li__strong"
                >Telefonszám *</label
              >
              <input
                type="tel"
                v-model="formData.phone"
                required
                class="form-input"
                placeholder="Gyors egyeztetéshez"
                :disabled="isSubmitting"
              />
            </div>
          </div>

          <button type="submit" class="submit-btn" :disabled="isSubmitting">
            <span class="btn-text" v-if="!isSubmitting">Időpont foglalása</span>
            <span class="btn-text" v-else>Küldés...</span>
          </button>
          <p class="page-color">
            <i class="supage-content__p__i">
              Az Időpont foglalása gombra kattintva automatikusan elfogadja az
              <NuxtLink class="supage-content__nlink" to="/adatvedelmi-tajekoztato">Adatvédelmi Szabályzatot.</NuxtLink>
            </i>
          </p>
          <!-- Success/Error Message -->
          <div
            v-if="submitMessage"
            class="submit-message"
            :class="{
              success: submitMessage.includes('✅'),
              error: submitMessage.includes('❌'),
            }"
          >
            {{ submitMessage }}
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
.main-title {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 20px;
  text-align: center;
}

.subpage {
  padding: 12em 5em 3em 5em;
}

.supage-content__nlink {
  color: #42b1ec;
}

.trust-banner {
  background: #000 url('/img/hero-left-bg.svg') no-repeat center/cover;
  color: white;
  padding: 3em;
  border-radius: 15px;
  margin-bottom: 30px;
  position: relative;
}

.trust-banner::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  border-radius: 15px;
  z-index: 1;
}

.trust-banner > * {
  position: relative;
  z-index: 2;
}

.trust-elements {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 15px;
  margin-top: 20px;
}

.trust-item {
  display: flex;
  align-items: center;
  gap: 10px;
  background: rgba(66, 177, 236, 0.2);
  padding: 15px;
  border-radius: 10px;
  border: 1px solid rgba(66, 177, 236, 0.3);
}

.trust-icon {
  font-size: 1.5rem;
}

.benefits-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  margin: 25px 0;
  padding: 1em 0;
}

.benefit-card {
  background: #f8f9fa;
  padding: 20px;
  border-radius: 10px;
  border-left: 4px solid #42b1ec;
}

.benefit-card h3 {
  color: #000;
  font-size: 1.2rem;
  margin-bottom: 10px;
}

.appointment-form {
  max-width: 800px;
  margin: 0 auto;
}

.submit-message {
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 20px;
  font-weight: bold;
  text-align: center;
}

.submit-message.success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.submit-message.error {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}

.form-section {
  background: #fff;
  padding: 25px;
  margin: 2.5em 0 2em 0;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.section-title {
  color: #000;
  font-size: 1.3rem;
  margin-bottom: 20px;
  border-bottom: 2px solid #42b1ec;
  padding-bottom: 10px;
}

.form-group {
  margin-bottom: 20px;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 12px;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 16px;
  transition: border-color 0.3s;
}

.form-select {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 16px;
  font-family: inherit;
  background-color: #fff;
  transition: all 0.3s ease;
  cursor: pointer;

  /* Custom arrow eltávolítása és saját hozzáadása */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;

  /* Saját nyíl hozzáadása */
  background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23666' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6,9 12,15 18,9'%3e%3c/polyline%3e%3c/svg%3e");
  background-repeat: no-repeat;
  background-position: right 12px center;
  background-size: 16px;
  padding-right: 45px;
}

.form-input:focus,
.form-textarea:focus {
  border-color: #42b1ec;
  outline: none;
}

.form-select:focus {
  border-color: #42b1ec;
  outline: none;
  box-shadow: 0 0 0 3px rgba(66, 177, 236, 0.1);

  /* Focus esetén kék nyíl */
  background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%2342b1ec' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6,9 12,15 18,9'%3e%3c/polyline%3e%3c/svg%3e");
}

.form-select:hover:not(:disabled) {
  border-color: #42b1ec;
  background-color: #fefefe;
}

.form-input:disabled,
.form-select:disabled {
  background-color: #f8f9fa;
  opacity: 0.6;
}

.form-select:disabled {
  cursor: not-allowed;

  /* Disabled állapotban szürke nyíl */
  background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23999' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6,9 12,15 18,9'%3e%3c/polyline%3e%3c/svg%3e");
}

.radio-group {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}

.radio-label {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
}

.radio-text {
  font-weight: normal;
}

.submit-btn {
  background: linear-gradient(135deg, #42b1ec 0%, #000 100%);
  color: white;
  border: none;
  padding: 20px 40px;
  border-radius: 10px;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  width: 100%;
  transition: transform 0.2s;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  background: linear-gradient(135deg, #000 0%, #42b1ec 100%);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-text {
  font-size: 1.1rem;
}

.btn-guarantee {
  font-size: 0.9rem;
  font-weight: normal;
  opacity: 0.9;
}

@media (max-width: 768px) {
  .subpage {
    padding: 8em 1.5em 2em 1.5em;
  }

  .trust-elements {
    grid-template-columns: 1fr;
  }

  .benefits-grid {
    grid-template-columns: 1fr;
  }

  .radio-group {
    flex-direction: column;
  }
  .trust-banner {
    padding: 2em;
  }
  .main-title {
    font-size: 1.5rem;
  }
  .subpage {
    padding: 9em 1.5em 1.5em 1.5em;
  }
}

@media (max-width: 480px) {
  .subpage {
    padding: 9em 1.5em 1.5em 1.5em;
  }
}

/* Safari specifikus javítások */
@supports (-webkit-appearance: none) {
  .form-select {
    /* Safari-ban a padding finomhangolása */
    padding-right: 40px;
  }
}

/* Firefox specifikus javítások */
@-moz-document url-prefix() {
  .form-select {
    /* Firefox-ban más padding kell */
    padding-right: 42px;
  }
}
</style>
