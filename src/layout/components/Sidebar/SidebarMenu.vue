<template>
  <a-menu theme="dark" mode="inline" :default-selected-keys="active">
    <template v-for="item in routes">
      <a-menu-item
        v-if="!item.hidden &&
          hasOneShowingChild(item.children,item) && (!onlyOneChild.children||onlyOneChild.noShowingChildren)&&!item.alwaysShow && onlyOneChild.meta "
        :key="resolvePath(item.path)"
      >
        <app-link :to="resolvePath(onlyOneChild.path)">
          <a-icon :type="onlyOneChild.meta.icon" />
          {{ onlyOneChild.meta.title }}
        </app-link>
      </a-menu-item>
      <a-sub-menu v-if="!item.hidden && item.meta" :key="resolvePath(item.path)">
        <span v-if="item.meta" slot="title">
          <a-icon :type="item.meta && item.meta.icon" />
          <span>{{ item.meta.title }}</span>
        </span>
        <a-menu-item
          v-for="child in item.children"
          :key="child.path"
          @click="toPath(item.path, child.path)"
        >
          {{ child.name }}
        </a-menu-item>
      </a-sub-menu>
    </template>
  </a-menu>
</template>

<script>
import path from 'path'
import { isExternal } from '@/utils/validate'
import AppLink from './Link'
import FixiOSBug from './FixiOSBug'

export default {
  name: 'SidebarItem',
  components: {
    AppLink
  },
  mixins: [FixiOSBug],
  props: {
    // route object
    routes: {
      type: Array,
      required: true
    },
    active: {
      type: Array,
      required: true
    }
  },
  data() {
    this.onlyOneChild = null
    return {}
  },
  methods: {
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
      if (isExternal(routePath)) {
        return routePath
      }
      return path.resolve(routePath)
    }
  }
}
</script>
