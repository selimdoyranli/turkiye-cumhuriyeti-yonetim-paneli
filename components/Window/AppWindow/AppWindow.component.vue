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

    // Economy
    fieldset.economy
      legend Ekonomi (Yeni!)
      .economy__columnsWrapper
        .interest-field-group
          // Interest
          .field-row
            strong Faiz
          .field-row
            input#interest(v-model="economy.interest" type="range" min="0" max="100")
            strong %{{ economy.interest }}

        .exchange-reserve-field-group
          // Exchange Reserve
          .field-row
            strong Döviz Rezervi
          .field-row
            input#exchangeReserve(v-model="economy.exchangeReserveRange" type="range" disabled value="0" max="0")
            strong ${{ economy.exchangeReserve.toLocaleString('tr-TR') }}
          .field-row
            button(@click="economy.exchangeReserveRange = 0; economy.exchangeReserve -= 10000000") Borçlan

      // USD
      .field-row
        strong Dolar
      .field-row
        input#usd(v-model="economy.usd" type="range" min="0" max="50")
        strong ₺{{ Number(economy.usd).toFixed(2) }}

      // EUR
      .field-row
        strong Euro
      .field-row
        input#eur(v-model="economy.eur" type="range" min="0" max="50")
        strong ₺{{ Number(economy.eur).toFixed(2) }}

      // Fire
      br
      br
      .field-row
        button(@click="economy.usd += 5; economy.eur += 5") Merkez bankası başkanını kov

    // Covid-19 & Banned Products
    fieldset
      legend Covid-19
      .field-row
        strong Sokağa çıkma yasağı
      .field-row
        .input-group
          input#yerli(type="checkbox")
          label(for="yerli") Yerli
        .input-group
          input#turist(type="checkbox")
          label(for="turist") Turist

      br
      br

      .field-row
        strong Satışı yasaklı ürünler
      .field-row.app-window__bannedProducts
        template(v-for="(product, index) in bannedProducts")
          .input-group
            input(type="checkbox" :id="product.title")
            label(:for="product.title") {{ product.title }}

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
    const bannedProducts = reactive([
      {
        title: 'Tarak',
        isChecked: true
      },
      {
        title: 'Ampul',
        isChecked: true
      },
      {
        title: 'Elektronik Eşya',
        isChecked: true
      },
      {
        title: 'Sigara',
        isChecked: true
      },
      {
        title: 'Alkol',
        isChecked: true
      },
      {
        title: 'Oyuncak',
        isChecked: true
      },
      {
        title: 'Kırtasiye',
        isChecked: true
      },
      {
        title: 'Aksesuar',
        isChecked: true
      },
      {
        title: 'Giyim',
        isChecked: true
      },
      {
        title: 'Ev Tekstili',
        isChecked: true
      },
      {
        title: 'Hırdavat',
        isChecked: true
      },
      {
        title: 'Züccaciye',
        isChecked: true
      },
      {
        title: 'Oto Aksesuar',
        isChecked: true
      },
      {
        title: 'Tuvalet Kağıdı',
        isChecked: true
      }
    ])

    const economy = reactive({
      interest: 14,
      exchangeReserve: -54600000000,
      exchangeReserveRange: 100,
      usd: 16.8,
      eur: 17.52
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

    return { bannedProducts, economy, close }
  }
})
</script>

<style lang="scss" src="./AppWindow.component.scss"></style>
