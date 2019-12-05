<template>
  <aside
    class="column is-2 is-narrow-mobile is-fullheight section is-hidden-mobile has-background-dark hero-body"
  >
    <p class="menu-label is-hidden-touch has-text-white">General</p>
    <ul class="menu-list">
      <li>
        <a
          href="#"
          :class="{ 'is-active': activeNum == 0 }"
          @click="changeActiveLink(0)"
        >
          <span class="icon"><i class="fa fa-home"></i></span> Home
        </a>
      </li>
      <li>
        <a
          href="#"
          :class="{ 'is-active': activeNum == 1 }"
          @click="changeActiveLink(1)"
        >
          <span class="icon"><i class="fa fa-home"></i></span> Home
        </a>
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  name: 'side_menu',
  data() {
    return {
      activeNum: 0
    }
  },
  methods: {
    changeActiveLink(n) {
      this.activeNum = n
    }
  }
}
</script>

<style scoped></style>
