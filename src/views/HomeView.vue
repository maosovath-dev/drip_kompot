<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue'
import HelloMessage from '../components/HelloMessage.vue'

const targetDate = new Date(2026, 11, 5)
const now = ref(Date.now())
const hasConfirmed = ref(false)
const showDetails = ref(false)
let timer

const countdown = computed(() => {
  const difference = Math.max(0, targetDate.getTime() - now.value)
  const seconds = Math.floor(difference / 1000)

  return {
    days: Math.floor(seconds / 86400),
    hours: Math.floor((seconds % 86400) / 3600),
    minutes: Math.floor((seconds % 3600) / 60),
    seconds: seconds % 60,
    isComplete: difference === 0
  }
})

onMounted(() => {
  timer = window.setInterval(() => {
    now.value = Date.now()
  }, 1000)
})

onUnmounted(() => {
  window.clearInterval(timer)
})
</script>

<template>
  <main class="page" :class="{ 'page-details': showDetails }">
    <section
      v-if="showDetails"
      class="details-card"
      aria-labelledby="details-title"
    >
      <header class="details-header">
        <div>
          <p class="details-kicker">កម្មវិធីដំណើរកម្សាន្ត</p>
          <h1 id="details-title" class="details-title">ថ្ងៃទី១ · ខេត្តកំពត</h1>
        </div>
        <p class="details-date">០៥ ធ្នូ ២០២៦</p>
      </header>

      <ol class="itinerary">
        <li class="itinerary-item">
          <time class="itinerary-time" datetime="06:30">៦:៣០ ព្រឹក</time>
          <div class="itinerary-content">
            <h2>ចេញដំណើរ</h2>
            <p>ចេញដំណើរពីភ្នំពេញ <br>(E-booking)</p>
          </div>
        </li>
        <li class="itinerary-item">
          <time class="itinerary-time" datetime="09:30">៩:៣០ ព្រឹក</time>
          <div class="itinerary-content">
            <h2>ឈប់សម្រាកពេលព្រឹក</h2>
            <p>សម្រាក និងរៀបចំខ្លួនបន្តដំណើរ</p>
          </div>
        </li>
        <li class="itinerary-item">
          <time class="itinerary-time" datetime="10:00">១០:០០ ព្រឹក</time>
          <div class="itinerary-content">
            <h2>ចាប់ផ្ដើមកម្មវិធីទស្សនាកម្សាន្ត</h2>
            <p>រីករាយជាមួយទីតាំងទេសចរណ៍នៅខេត្តកំពត</p>
          </div>
        </li>
        <li class="itinerary-item">
          <time class="itinerary-time" datetime="11:00">១១:០០ ព្រឹក</time>
          <div class="itinerary-content">
            <h2>ចូលស្នាក់នៅ</h2>
            <p>Check-in នៅផ្ទះសំណាក់</p>
          </div>
        </li>
        <li class="itinerary-item">
          <time class="itinerary-time" datetime="12:00">១២:០០–១:៣០ រសៀល</time>
          <div class="itinerary-content">
            <h2>អាហារថ្ងៃត្រង់ និងសម្រាក</h2>
            <p>ទទួលទានអាហារថ្ងៃត្រង់ និងសម្រាកត្រៀមកម្មវិធីបន្ទាប់</p>
          </div>
        </li>
        <li class="itinerary-item">
          <time class="itinerary-time" datetime="14:00">២:០០ រសៀល</time>
          <div class="itinerary-content">
            <h2>បន្តដំណើរកម្សាន្ត</h2>
            <p>ចូលរួមកម្មវិធីទេសចរណ៍ពេលរសៀល</p>
          </div>
        </li>
        <li class="itinerary-item">
          <time class="itinerary-time" datetime="18:00">៦:០០ ល្ងាច</time>
          <div class="itinerary-content">
            <h2>អាហារពេលល្ងាច</h2>
            <p>ទទួលទានអាហារ និងសម្រាកនៅកន្លែងស្នាក់នៅ</p>
          </div>
        </li>
      </ol>

      <div class="details-actions">
        <button class="action-button back-button" type="button" @click="showDetails = false">
          ត្រឡប់ក្រោយ
        </button>
        <button
          v-if="!hasConfirmed"
          class="action-button confirm-button"
          type="button"
          @click="hasConfirmed = true; showDetails = false"
        >
          ខ្ញុំចូលរួមដំណើរកម្សាន្ត
        </button>
      </div>
    </section>

    <section
      v-else-if="hasConfirmed"
      class="confirmation-card"
      aria-labelledby="confirmation-title"
      aria-live="polite"
    >
      <span class="confirmation-check" aria-hidden="true">✓</span>
      <p class="confirmation-kicker">កំពត · កម្ពុជា</p>
      <h1 id="confirmation-title" class="confirmation-title">អ្នកបានចុចរួចហើយ!</h1>
      <p class="confirmation-copy">
        អ្នកបានបញ្ជាក់ថានឹងទៅដំណើរកម្សាន្តជាមួយពួកយើងហើយ។
      </p>
      <p class="confirmation-date">ថ្ងៃសៅរ៍ ទី៥ ខែធ្នូ ឆ្នាំ២០២៦</p>
      <p class="confirmation-reminder">កុំឱ្យខកខានណា! កំពតកំពុងរង់ចាំអ្នក។</p>
      <button class="action-button details-button" type="button" @click="showDetails = true">
        ព័ត៌មានលម្អិតកម្មវិធី
      </button>
      <button class="action-button back-button" type="button" @click="hasConfirmed = false">
        មើលម៉ោងរាប់ថយក្រោយ
      </button>
    </section>

    <section v-else class="countdown-card" aria-labelledby="countdown-title">
      <div class="destination-panel">
        <p class="destination-badge">
          <span class="location-dot" aria-hidden="true"></span>
          កំពត · កម្ពុជា
        </p>
        <HelloMessage text="ដំណើរកម្សាន្តទៅកាន់ខេត្តកំពត" />
        <p class="destination-copy">
          ត្រៀមខ្លួនសម្រាប់ដំណើរកម្សាន្តដ៏ស្រស់ស្អាត ជាមួយធម្មជាតិ និងសមុទ្រកម្ពុជា។
        </p>
      </div>

      <div class="timer-panel">
        <p class="eyebrow">ដំណើរកម្សាន្តចាប់ផ្ដើមក្នុង</p>
        <h2 id="countdown-title" class="countdown-title">
          ថ្ងៃសៅរ៍ ទី៥ ខែធ្នូ ឆ្នាំ២០២៦
        </h2>

        <p v-if="countdown.isComplete" class="complete-message" role="status">
          ដល់ថ្ងៃកំណត់ហើយ!
        </p>
        <div v-else class="time-grid" aria-label="ពេលវេលាដែលនៅសល់">
          <div class="time-unit">
            <span class="time-value">{{ countdown.days }}</span>
            <span class="time-label">ថ្ងៃ</span>
          </div>
          <div class="time-unit">
            <span class="time-value">{{ countdown.hours }}</span>
            <span class="time-label">ម៉ោង</span>
          </div>
          <div class="time-unit">
            <span class="time-value">{{ countdown.minutes }}</span>
            <span class="time-label">នាទី</span>
          </div>
          <div class="time-unit">
            <span class="time-value">{{ countdown.seconds }}</span>
            <span class="time-label">វិនាទី</span>
          </div>
        </div>
        <p v-if="!countdown.isComplete" class="supporting-text">
          នៅសល់ពេលប៉ុន្មានទៀតដល់ថ្ងៃដែលអ្នករង់ចាំ
        </p>
        <div class="trip-actions">
          <button class="action-button details-button" type="button" @click="showDetails = true">
            ព័ត៌មានលម្អិត
          </button>
          <button class="action-button confirm-button" type="button" @click="hasConfirmed = true">
            ខ្ញុំចូលរួមដំណើរកម្សាន្ត
          </button>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.page {
  box-sizing: border-box;
  display: grid;
  min-height: 100vh;
  place-items: center;
  padding: 24px;
  background-color: #163d4b;
  background-image:
    linear-gradient(90deg, rgb(6 25 37 / 70%), rgb(6 25 37 / 20%)),
    url('/images/kampot-background.png');
  background-position: center, center 56%;
  background-size: cover;
  background-repeat: no-repeat;
}

.page-details {
  height: 100vh;
  height: 100dvh;
  min-height: 0;
  overflow: hidden;
}

.countdown-card {
  display: grid;
  grid-template-columns: minmax(0, 0.9fr) minmax(0, 1.1fr);
  width: min(100%, 1020px);
  overflow: hidden;
  border: 1px solid rgb(255 255 255 / 38%);
  border-radius: 30px;
  background: rgb(10 34 49 / 74%);
  box-shadow: 0 28px 80px rgb(0 16 28 / 35%);
  -webkit-backdrop-filter: blur(14px);
  backdrop-filter: blur(14px);
}

.destination-panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: clamp(32px, 5vw, 64px);
  color: #fff;
  text-align: left;
}

.destination-badge {
  display: inline-flex;
  align-items: center;
  align-self: flex-start;
  gap: 9px;
  margin: 0;
  padding: 9px 14px;
  border: 1px solid rgb(255 255 255 / 35%);
  border-radius: 999px;
  background: rgb(255 255 255 / 12%);
  color: #fff;
  font-size: 0.9rem;
  font-weight: 600;
}

.location-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #e9b85b;
  box-shadow: 0 0 0 4px rgb(233 184 91 / 20%);
}

.destination-panel :deep(.title) {
  margin: 22px 0 12px;
  color: #fff;
  font-size: clamp(2rem, 4vw, 3rem);
  line-height: 1.35;
  text-shadow: 0 2px 18px rgb(0 0 0 / 22%);
}

.destination-copy {
  max-width: 360px;
  margin: 0;
  color: rgb(255 255 255 / 84%);
  font-size: 1rem;
  line-height: 1.9;
}

.eyebrow {
  margin: 0 0 10px;
  color: #ae7b22;
  font-size: 0.95rem;
  font-weight: 700;
}

.timer-panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: clamp(32px, 5vw, 56px);
  background: rgb(255 255 255 / 96%);
  text-align: center;
}

.countdown-title {
  margin: 0 0 28px;
  color: #233d35;
  font-size: clamp(1.1rem, 2.4vw, 1.4rem);
  font-weight: 600;
}

.time-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 10px;
}

.time-unit {
  position: relative;
  display: flex;
  min-height: 108px;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  border: 1px solid #e7ece8;
  border-radius: 16px;
  background: #fff;
  box-shadow: 0 8px 20px rgb(27 68 51 / 6%);
}

.time-unit::before {
  position: absolute;
  top: 0;
  width: 30px;
  height: 3px;
  border-radius: 0 0 4px 4px;
  background: #c99a45;
  content: '';
}

.time-value {
  color: #18523d;
  font-size: clamp(1.8rem, 6vw, 2.8rem);
  font-variant-numeric: tabular-nums;
  font-weight: 700;
  line-height: 1;
}

.time-label {
  color: #77827a;
  font-size: 0.95rem;
}

.supporting-text {
  margin: 22px 0 0;
  color: #727c75;
  font-size: 0.95rem;
}

.complete-message {
  margin: 36px 0 12px;
  color: #18523d;
  font-size: 1.5rem;
  font-weight: 700;
}

.action-button {
  border: 0;
  border-radius: 999px;
  background: linear-gradient(135deg, #16583e, #287853);
  box-shadow: 0 10px 24px rgb(22 88 62 / 20%);
  color: #fff;
  cursor: pointer;
  font: inherit;
  font-weight: 700;
  padding: 14px 22px;
  transition: box-shadow 160ms ease, transform 160ms ease;
}

.action-button:hover {
  box-shadow: 0 14px 28px rgb(22 88 62 / 28%);
  transform: translateY(-2px);
}

.action-button:focus-visible {
  outline: 3px solid #d5a448;
  outline-offset: 4px;
}

.confirm-button {
  background: linear-gradient(135deg, #16583e, #287853);
}

.details-button {
  border: 1px solid #cbd9cf;
  background: #fff;
  box-shadow: none;
  color: #18523d;
}

.details-button:hover {
  background: #f3f7f3;
  box-shadow: 0 8px 18px rgb(22 88 62 / 10%);
}

.trip-actions,
.details-actions {
  display: grid;
  gap: 12px;
  width: min(100%, 340px);
  margin: 24px auto 0;
}

.details-card {
  display: flex;
  flex-direction: column;
  width: min(100%, 800px);
  height: calc(100vh - 48px);
  height: calc(100dvh - 48px);
  box-sizing: border-box;
  overflow: hidden;
  padding: clamp(24px, 5vw, 48px);
  border: 1px solid rgb(255 255 255 / 70%);
  border-radius: 30px;
  background: rgb(255 255 255 / 97%);
  box-shadow: 0 28px 80px rgb(0 16 28 / 35%);
}

.details-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 24px;
}

.details-kicker {
  margin: 0 0 6px;
  color: #ae7b22;
  font-weight: 700;
}

.details-title {
  margin: 0;
  color: #18523d;
  font-size: clamp(1.5rem, 4vw, 2rem);
}

.details-date {
  flex: none;
  margin: 0;
  padding: 10px 14px;
  border-radius: 999px;
  background: #f3f6f1;
  color: #405c4c;
  font-size: 0.9rem;
  font-weight: 700;
}

.itinerary {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  grid-template-rows: repeat(4, minmax(0, 1fr));
  grid-auto-flow: column;
  flex: 1;
  min-height: 0;
  gap: 0 24px;
  margin: 0;
  padding: 0;
  list-style: none;
  overflow: hidden;
}

.itinerary-item {
  display: grid;
  grid-template-columns: minmax(128px, 0.32fr) minmax(0, 1fr);
  gap: 18px;
  align-content: center;
  padding: 8px 0;
  border-top: 1px solid #e8eee9;
}

.itinerary-time {
  padding-top: 2px;
  color: #ae7b22;
  font-size: 0.95rem;
  font-weight: 700;
}

.itinerary-content h2 {
  margin: 0 0 4px;
  color: #233d35;
  font-size: 1rem;
}

.itinerary-content p {
  margin: 0;
  color: #65736a;
  font-size: 0.95rem;
  line-height: 1.7;
}

.details-actions {
  display: flex;
  width: 100%;
  flex: none;
}

.details-actions .action-button {
  flex: 1;
}

.confirmation-card {
  width: min(100%, 620px);
  box-sizing: border-box;
  padding: clamp(32px, 7vw, 64px);
  border: 1px solid rgb(255 255 255 / 70%);
  border-radius: 30px;
  background: rgb(255 255 255 / 96%);
  box-shadow: 0 28px 80px rgb(0 16 28 / 35%);
  text-align: center;
}

.confirmation-check {
  display: grid;
  width: 76px;
  height: 76px;
  margin: 0 auto 20px;
  place-items: center;
  border-radius: 50%;
  background: #e5f2e9;
  color: #18523d;
  font-size: 2.5rem;
  font-weight: 700;
}

.confirmation-kicker {
  margin: 0 0 10px;
  color: #ae7b22;
  font-weight: 700;
}

.confirmation-title {
  margin: 0;
  color: #18523d;
  font-size: clamp(1.7rem, 5vw, 2.5rem);
}

.confirmation-copy {
  margin: 16px 0;
  color: #58675e;
  line-height: 1.8;
}

.confirmation-date {
  margin: 20px 0;
  padding: 14px;
  border-radius: 14px;
  background: #f3f6f1;
  color: #233d35;
  font-weight: 700;
}

.confirmation-reminder {
  margin: 0 0 24px;
  color: #ae7b22;
  font-weight: 700;
}

.confirmation-card .details-button,
.confirmation-card .back-button {
  width: min(100%, 340px);
}

.confirmation-card .back-button {
  margin-top: 12px;
}

@media (max-height: 700px) and (min-width: 761px) {
  .details-card {
    padding: 20px 32px;
  }

  .details-header {
    margin-bottom: 10px;
  }

  .itinerary-item {
    padding: 4px 0;
  }

  .itinerary-content p {
    display: none;
  }

  .details-actions {
    margin-top: 10px;
  }
}

@media (max-width: 760px) {
  .countdown-card {
    grid-template-columns: 1fr;
    max-width: 620px;
  }

  .destination-panel {
    align-items: center;
    padding: 34px 32px 28px;
    text-align: center;
  }

  .destination-panel :deep(.title) {
    margin-top: 18px;
  }

  .destination-copy {
    max-width: 460px;
  }

  .timer-panel {
    padding: 30px 32px 36px;
  }
}

@media (max-width: 480px) {
  .page {
    padding: 16px;
  }

  .countdown-card {
    border-radius: 24px;
  }

  .destination-panel {
    padding: 30px 22px 22px;
  }

  .timer-panel {
    padding: 26px 18px 30px;
  }

  .time-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 10px;
  }

  .time-unit {
    min-height: 88px;
    border-radius: 14px;
  }

  .confirm-button,
  .back-button,
  .details-button {
    width: 100%;
  }

  .details-card {
    height: calc(100vh - 32px);
    height: calc(100dvh - 32px);
    padding: 20px;
    border-radius: 24px;
  }

  .details-header {
    align-items: center;
    margin-bottom: 8px;
  }

  .itinerary {
    grid-template-columns: minmax(0, 1fr);
    grid-template-rows: repeat(7, minmax(0, 1fr));
    grid-auto-flow: row;
    gap: 0;
  }

  .itinerary-item {
    grid-template-columns: minmax(88px, 0.32fr) minmax(0, 1fr);
    gap: 10px;
    padding: 4px 0;
  }

  .itinerary-time {
    font-size: 0.82rem;
  }

  .itinerary-content h2 {
    font-size: 0.88rem;
    line-height: 1.35;
  }

  .itinerary-content p {
    display: none;
  }

  .details-actions {
    flex-direction: column;
    margin-top: 10px;
    gap: 8px;
  }
}

@media (max-width: 480px) {
  .details-card {
    padding: 14px;
  }

  .details-title {
    font-size: 1.2rem;
  }

  .details-date {
    padding: 8px 10px;
    font-size: 0.8rem;
  }
}
</style>
