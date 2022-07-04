<template lang="pug">
.window.app-window
  .title-bar
    .title-bar-text 2023.exe
    .title-bar-controls
      button(aria-label="Minimize")
      button(aria-label="Maximize")
      button(aria-label="Close" @click="close")
  .window-body
    .app-window__head
      h4.app-window__title TÜRKİYE CUMHURİYETİ YÖNETİM PANELİ
      span.app-window__version v2022.04.07

    // Defector Control
    fieldset
      legend Mülteci Kontrol (Yeni!)
      .field-row
        strong Sınır kapısı
      .field-row
        .input-group
          input#sinir-kapisi(type="checkbox" checked @click.prevent)
          label(for="sinir-kapisi") Açık/Kapalı

      br
      br

      .field-row
        strong Kabul edilecek ülkeler
      .field-row.app-window__countries
        template(v-for="(country, index) in countries")
          .input-group
            input(type="checkbox" :id="country.title" :checked="country.isChecked")
            label(:for="country.title") {{ country.title }}

    // Economy
    fieldset.economy
      legend Ekonomi
      .economy__columnsWrapper
        .field-group
          // Interest
          .field-row
            strong Faiz
          .field-row
            input#interest(v-model="economy.interest" type="range" min="0" max="100")
            strong %{{ economy.interest }}
          // Fire
          br
          .field-row
            button(@click="economy.usd += 5; economy.eur += 5") Merkez bankası başkanını kov

        .field-group
          // Exchange Reserve
          .field-row
            strong Döviz Rezervi
          .field-row
            input#exchangeReserve(v-model="economy.exchangeReserveRange" type="range" disabled value="0" max="0")
            strong ${{ economy.exchangeReserve.toLocaleString('tr-TR') }}
          .field-row
            br
            button.ml-auto(@click="economy.exchangeReserveRange = 0; economy.exchangeReserve -= 10000000") Borçlan

        .field-group
          br
          br
          // USD
          .field-row
            strong Dolar
          .field-row
            input#usd(v-model="economy.usd" type="range" min="0" max="50")
            strong ₺{{ Number(economy.usd).toFixed(2) }}

        .field-group
          br
          br
          // Gas
          .field-row
            strong Benzin
          .field-row
            input#gas(v-model="economy.gas" type="range" min="0" max="100")
            strong ₺{{ Number(economy.gas).toFixed(2) }}

        .field-group
          // EUR
          .field-row
            strong Euro
          .field-row
            input#eur(v-model="economy.eur" type="range" min="0" max="50")
            strong ₺{{ Number(economy.eur).toFixed(2) }}

        .field-group
          // Diesel
          .field-row
            strong Motorin
          .field-row
            input#diesel(v-model="economy.diesel" type="range" min="0" max="100")
            strong ₺{{ Number(economy.diesel).toFixed(2) }}

    // Shortcuts
    fieldset.shortcuts
      legend Sık Kullanılan Kısayollar
      .field-row
        .row
          button Random Vergi Arttır
          button Çay Fırlat
          button Kongre Yap
          button Mağdur Ol
          button Kabineyi Değiş
        .row
          button Yerli Otomobili Duyur
          button Ay'a Araç Gönder
          button Kemal'e Salla
          button Ekrem'e Salla
          button Random Salla
</template>

<script>
import { defineComponent, reactive, watch } from '@nuxtjs/composition-api'

export default defineComponent({
  setup() {
    const countries = reactive([
      {
        title: 'Suriye',
        isChecked: true
      },
      {
        title: 'Afganistan',
        isChecked: true
      },
      {
        title: 'Pakistan',
        isChecked: true
      },
      {
        title: 'Irak',
        isChecked: true
      },
      {
        title: 'İran',
        isChecked: true
      },
      {
        title: 'Ürdün',
        isChecked: true
      },
      {
        title: 'Yemen',
        isChecked: true
      },
      {
        title: 'Güney Sudan',
        isChecked: true
      },
      {
        title: 'Myanmar',
        isChecked: true
      },
      {
        title: 'Zimbabwe',
        isChecked: true
      },
      {
        title: 'Çeçenistan',
        isChecked: true
      }
    ])

    const economy = reactive({
      interest: 14,
      exchangeReserve: -54600000000,
      exchangeReserveRange: 100,
      usd: 16.8,
      eur: 17.52,
      gas: 25.17,
      diesel: 26.65
    })

    watch(
      () => economy.interest,
      (currentValue, oldValue) => {
        if (currentValue > oldValue) {
          economy.usd -= 3
          economy.eur -= 3
        } else {
          economy.usd += 3
          economy.eur += 3
        }
      }
    )

    const close = () => {
      window.alert('Daha beraber yürüyecektik biz bu yollarda?')
    }

    return { countries, economy, close }
  }
})
</script>

<style lang="scss" src="./AppWindow.component.scss"></style>
