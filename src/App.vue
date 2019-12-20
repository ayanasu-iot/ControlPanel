<template>
  <div id="app">
      <Title />
      <div class="main-content columns is-fullheight">
        <Menu />
        <div class="container column is-10">
          <Body />
          <Gallery />
        </div>
      </div>
    </div>
</template>

<script>
import Title from './components/title_header.vue'
import Body from './components/upload_form.vue'
import Menu from './components/side_menu.vue'
import Gallery from './components/gallery.vue'

export default {
  name: 'app',
  components: {
    Title,
    Body,
    Menu,
    Gallery
  }
}
</script>

<style lang="scss">
@import '~bulma/bulma.sass';
</style>
