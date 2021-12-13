<template lang="pug">
.page.main-page
  AppWindow
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'
import { AppWindow } from '@/components/Window'

export default defineComponent({
  components: {
    AppWindow
  },
  setup() {},
  head: {
    title: 'Türkiye Cumhuriyeti Yönetim Paneli',
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: `Siz bu kardeşinize password'u verin`
      }
    ]
  }
})
</script>

<style lang="scss" scoped>
.page {
  position: relative;
}
</style>
