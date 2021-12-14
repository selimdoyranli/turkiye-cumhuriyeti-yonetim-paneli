<template lang="pug">
#taskbar.app-task-bar
  .background.sliced.vertical
    .row.top
    .row.middle
    .row.bottom
  #start-button
    .container
      .background.sliced
        .column.left
          .row.top
          .row.middle
          .row.bottom
        .column.middle
          .row.top
          .row.middle
          .row.bottom
        .column.right
          .row.top
          .row.middle
          .row.bottom
      .content
        span.icon
          img(src="@/assets/img/elements/start-menu-logo.png")
        span.text Başlat
      .overlay(title="Başlat")
  #task-band
  #tray-notify
    .container
      .background.sliced
        .column.left
          .row.top
          .row.middle
          .row.bottom
        .column.middle
          .row.top
          .row.middle
          .row.bottom
        .column.right
          .row.top
          .row.middle
          .row.bottom
      .content
        .clock
          .text {{ new Date(Date.now()).getHours() }}:{{ new Date(Date.now()).getMinutes() }}
          .overlay(title="segunda-feira, 8 de abril de 2019")
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'

export default defineComponent({
  setup() {}
})
</script>

<style lang="scss" src="./AppTaskBar.component.scss"></style>
