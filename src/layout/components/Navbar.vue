<template>
  <div class="navbar">
    <hamburger
      id="hamburger-container"
      :is-active="sidebar.opened"
      class="hamburger-container"
      @toggleClick="toggleSideBar"
    />

    <breadcrumb id="breadcrumb-container" class="breadcrumb-container" />

    <div class="right-menu">
      <a-dropdown v-if="name" placement="bottomRight">
        <span class="avatar-wrapper">
          <a-avatar size="small" :src="avatar" class="user-avatar" />
          <span>{{ name }}</span>
        </span>
        <template v-slot:overlay>
          <a-menu class="ant-pro-drop-down menu" :selected-keys="[]">
            <a-menu-item key="github">
              <a href="https://github.com/TyCoding/ant-design-vue-pro" target="_blank">
                <a-icon type="github" />
                Github
              </a>
            </a-menu-item>
            <a-menu-item key="Blog">
              <a href="https://github.com/TyCoding" target="_blank">
                <a-icon type="link" />
                Blog
              </a>
            </a-menu-item>
            <a-menu-divider />
            <a-menu-item key="center">
              <a-icon type="user" />
              个人中心
            </a-menu-item>
            <a-menu-item key="settings">
              <a-icon type="setting" />
              个人设置
            </a-menu-item>
            <a-menu-divider />
            <a-menu-item key="logout">
              <a-icon type="logout" />
              退出登录
            </a-menu-item>
          </a-menu>
        </template>
      </a-dropdown>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Breadcrumb from '@/components/Breadcrumb'
import Hamburger from '@/components/Hamburger'

export default {
  components: {
    Breadcrumb,
    Hamburger
  },
  computed: {
    ...mapGetters([
      'sidebar',
      'avatar',
      'device',
      'name'
    ])
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('app/toggleSideBar')
    },
    async logout() {
      await this.$store.dispatch('user/logout')
      this.$router.push(`/login?redirect=${this.$route.fullPath}`)
    }
  }
}
</script>

<style lang="less" scoped>

  .navbar {
    height: 64px;
    overflow: hidden;
    position: relative;
    background: #fff;
    box-shadow: 0 1px 4px rgba(0, 21, 41, .08);

    .hamburger-container {
      line-height: 64px;
      height: 100%;
      float: left;
      cursor: pointer;
      transition: background .3s;
      -webkit-tap-highlight-color: transparent;

      &:hover {
        background: rgba(0, 0, 0, .025)
      }
    }

    .breadcrumb-container {
      float: left;
    }

    .errLog-container {
      display: inline-block;
      vertical-align: top;
    }

    .right-menu {
      float: right;
      height: 100%;
      line-height: 64px;

      &:focus {
        outline: none;
      }

      .right-menu-item {
        display: inline-block;
        padding: 0 8px;
        height: 100%;
        font-size: 18px;
        color: #5a5e66;
        vertical-align: text-bottom;

        &.hover-effect {
          cursor: pointer;
          transition: background .3s;

          &:hover {
            background: rgba(0, 0, 0, .025)
          }
        }
      }

      .avatar-wrapper {
        display: inline-block;
        height: 100%;
        padding: 0 12px;
        cursor: pointer;
        -webkit-transition: all .3s;
        transition: all .3s;
        line-height: 64px;
        vertical-align: top;

        &:hover {
          background: rgba(0, 0, 0, .025);
        }
      }
    }
  }
</style>
