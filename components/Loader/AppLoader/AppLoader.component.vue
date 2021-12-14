<template lang="pug">
.app-loader
  .logo
    p.top Microsoft
    p.mid Windows
      span XP
    p.bottom 2023 Edition
  .container
    .box
    .box
    .box
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'

export default defineComponent({
  setup() {}
})
</script>

<style lang="scss" src="./AppLoader.component.scss"></style>
