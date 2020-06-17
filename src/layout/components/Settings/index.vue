<template>
  <div class="setting-drawer-index-content">
    <div :style="{ marginBottom: '24px' }">
      <h3 class="setting-drawer-index-title">其他设置</h3>
      <div>
        <a-list :split="false">
          <a-list-item>
            <a-switch slot="actions" size="small" v-model="fixedHeader" />
            <a-list-item-meta>
              <div slot="title">固定 Header</div>
            </a-list-item-meta>
          </a-list-item>
          <a-list-item>
            <a-switch slot="actions" size="small" v-model="sidebarLogo" />
            <a-list-item-meta>
              <div slot="title">侧边栏 Logo</div>
            </a-list-item-meta>
          </a-list-item>
        </a-list>
      </div>
    </div>
    <a-divider />
    <div :style="{ marginBottom: '24px' }">
      <a-alert type="warning" :style="{ marginTop: '24px' }">
        <span slot="message">
          项目源码：
          <a href="https://github.com/TyCoding/ant-design-vue-pro" target="_blank">https://github.com/TyCoding/ant-design-vue-pro</a>
        </span>
      </a-alert>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return { }
  },
  computed: {
    fixedHeader: {
      get() {
        return this.$store.state.settings.fixedHeader
      },
      set(val) {
        this.$store.dispatch('settings/changeSetting', {
          key: 'fixedHeader',
          value: val
        })
      }
    },
    sidebarLogo: {
      get() {
        return this.$store.state.settings.sidebarLogo
      },
      set(val) {
        this.$store.dispatch('settings/changeSetting', {
          key: 'sidebarLogo',
          value: val
        })
      }
    }
  }
}
</script>

<style lang="less" scoped>
  a {
    color: #1890ff;
  }
</style>
