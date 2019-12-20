<template>
  <CSidebar
    fixed
    :minimize="minimize"
    :show.sync="show"
  >
    <CSidebarBrand
      :imgFull="{ width: 30, height: 30, alt: 'Logo', src: 'img/happy/logo.png'}"
      :imgMinimized="{ width: 30, height: 30, alt: 'Logo', src: 'img/happy/logo.png'}"
      :wrappedInLink="{ href: '/dashboard', target: '_blank'}"
    />
    <CRenderFunction flat :content-to-render="nav"/>
    <CSidebarMinimizer
      class="d-md-down-none"
      @click.native="minimize = !minimize"
    />
  </CSidebar>
</template>

<script>
import nav from './_nav'

export default {
  name: 'TheSidebar',
  data () {
    return {
      minimize: false,
      nav,
      show: 'responsive'
    }
  },
  mounted () {
    this.$root.$on('toggle-sidebar', () => {
      const sidebarOpened = this.show === true || this.show === 'responsive'
      this.show = sidebarOpened ? false : 'responsive'
    })
    this.$root.$on('toggle-sidebar-mobile', () => {
      const sidebarClosed = this.show === 'responsive' || this.show === false
      this.show = sidebarClosed ? true : 'responsive'
    })
  }
}
</script>
