<template>
  <div id="app">
    <Title />
    <div class="main-content columns is-fullheight">
      <Menu />
      <Body />
    </div>
  </div>
</template>

<script>
import Title from './components/title_header.vue'
import Body from './components/upload_form.vue'
import Menu from './components/side_menu.vue'

export default {
  name: 'app',
  components: {
    Title,
    Body,
    Menu
  }
}
</script>

<style lang="scss">
@import '~bulma/bulma.sass';
</style>
