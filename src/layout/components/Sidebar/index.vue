<template>
  <a-layout-sider v-model="isCollapse" width="256px" :trigger="null" collapsible>
    <logo v-if="showLogo" :collapse="isCollapse" />
    <sidebar-menu :routes="permission_routes" :active="[activeMenu]" />
  </a-layout-sider>
</template>

<script>
import { mapGetters } from 'vuex'
import Logo from './Logo'
import SidebarMenu from './SidebarMenu'
import variables from '@/styles/variables.less'

export default {
  components: { SidebarMenu, Logo },
  computed: {
    ...mapGetters([
      'permission_routes',
      'sidebar'
    ]),
    activeMenu() {
      const route = this.$route
      const { meta, path } = route
      // if set path, the sidebar will highlight the path you set
      if (meta.activeMenu) {
        return meta.activeMenu
      }
      return path
    },
    showLogo() {
      return this.$store.state.settings.sidebarLogo
    },
    variables() {
      return variables
    },
    isCollapse() {
      return !this.sidebar.opened
    }
  }
}
</script>
