<template>
  <main class="flex flex-col justify-center h-full mx-auto max-w-600px">
    <section class="flex flex-col items-center leading-loose text-center">
      <div class="text-3xl">
        <span class="i-twemoji-christmas-tree"></span>
        {{ t('happyHolidays') }}
        <span class="i-twemoji-world-map"></span>
      </div>

      <i18n-t keypath="christmasIsComing" tag="span">
        <template #date>
          {{ d(christmasDate, 'long') }}
        </template>
        <template #time>
          <span class="font-bold text-green">{{ t('day', days) }}</span>
        </template>
      </i18n-t>

      <div class="flex items-center justify-evenly w-200px">
        <button @click="changeLocale" class="icon-button">
          <span class="i-carbon-language" />
        </button>
        <p>
          <span :class="flags[locale]" />
          <span>{{ t('language') }}</span>
        </p>
      </div>
    </section>
  </main>
</template>

<script setup>
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'

const { t, d, locale, availableLocales: locales } = useI18n()

const christmasDate = new Date('2022/12/25')

const days = computed(() =>
  Math.ceil((christmasDate.getTime() - new Date()) / 86400000)
)

const changeLocale = () => {
  const index = locales.findIndex(l => l === locale.value)
  const nextIndex = (index + 1) % locales.length
  locale.value = locales[nextIndex]
}

const flags = {
  de: 'i-twemoji-flag-germany',
  en: 'i-twemoji-flag-united-states',
  fr: 'i-twemoji-flag-france',
  'ja-JP': 'i-twemoji-flag-japan',
}
</script>

<style scoped>
.icon-button {
  @apply text-xl
    w-32px
    h-32px
    rounded-full
    border-1
    border-transparent
    bg-transparent
    cursor-pointer
    duration-300
    hover:ring-2
    hover:border-green-500
    hover:ring-green-500
    hover:ring-opacity-40
    hover:text-green-600;
}
</style>
