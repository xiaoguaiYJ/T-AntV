<template>
  <a-layout-sider v-model="isCollapse" width="256px" :trigger="null" collapsible>
    <logo v-if="showLogo" :collapse="isCollapse" />
    <s-menu :collapsed="isCollapse" :menu="permission_routes" style="padding: 16px 0px;" @select="onSelect" />
  </a-layout-sider>
</template>

<script>
import { mapGetters } from 'vuex'
import Logo from './Logo'
import variables from '@/styles/variables.less'
import path from 'path'
import SMenu from './Menu/index'
import { isExternal } from '@/utils/validate'

export default {
  components: {
    Logo,
    SMenu
  },
  data() {
    this.onlyOneChild = null
    return {
      openKeys: [],
      selectedKeys: ['2', '2.1', '2.1.1']
    }
  },
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
  },
  methods: {
    onSelect(obj) {
      this.$emit('menuSelect', obj)
    },
    onOpenChange(openKeys) {
      this.openKeys = openKeys
    },
    // SideBar Item Router jump
    toPath(basePath, toPath) {
      this.$router.push(path.resolve(basePath, toPath))
    },
    hasOneShowingChild(children = [], parent) {
      const showingChildren = children.filter(item => {
        if (item.hidden) {
          return false
        } else {
          // Temp set(will be used if only has one showing child)
          this.onlyOneChild = item
          return true
        }
      })

      // When there is only one child router, the child router is displayed by default
      if (showingChildren.length === 1) {
        return true
      }

      // Show parent if there are no child router to display
      if (showingChildren.length === 0) {
        this.onlyOneChild = { ...parent, path: '', noShowingChildren: true }
        return true
      }

      return false
    },
    resolvePath(routePath) {
      const basePath = this.$route.path
      if (isExternal(routePath)) {
        return routePath
      }
      return path.resolve(basePath, routePath)
    }
  }
}
</script>
