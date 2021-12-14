<template lang="pug">
.page.main-page
  AppLoader(v-if="isLoadingApp")
  AppWindow
  AppTaskBar
</template>

<script>
import { defineComponent, onMounted, ref } from '@nuxtjs/composition-api'
import { AppLoader } from '@/components/Loader'
import { AppWindow } from '@/components/Window'
import { AppTaskBar } from '@/components/Bar'

export default defineComponent({
  components: {
    AppLoader,
    AppWindow,
    AppTaskBar
  },
  setup() {
    const isLoadingApp = ref(true)

    onMounted(() => {
      setTimeout(() => {
        isLoadingApp.value = false
      }, 4000)
    })

    return { isLoadingApp }
  },
  head: {
    title: 'Türkiye Cumhuriyeti Yönetim Paneli',
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: `Siz bu kardeşinize password'u verin...`
      },
      { hid: 'og:title', name: 'og:title', content: 'Türkiye Cumhuriyeti Yönetim Paneli' },
      { hid: 'og:description', name: 'og:description', content: `Siz bu kardeşinize password'u verin...` },
      { hid: 'og:image', name: 'og:image', content: `https://turkiyecumhuriyetiyonetimpaneli.vercel.app/meta.jpg` },
      { hid: 'twitter:card', name: 'twitter:card', content: `summary_large_image` },
      { hid: 'twitter:image', name: 'twitter:image', content: `https://turkiyecumhuriyetiyonetimpaneli.vercel.app/meta.jpg` }
    ]
  }
})
</script>

<style lang="scss" scoped>
.page {
  position: relative;
  max-width: 1024px;
  min-height: calc(100vh - 6rem);
  margin: 0 auto;
  padding: 3rem 0;
  background-image: url('~/assets/img/elements/bg.jpg');
  background-position: center center;
  background-size: cover;
}
</style>
