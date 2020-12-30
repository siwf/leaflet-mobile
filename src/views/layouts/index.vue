<template>
  <div class="app-container">
    <div class="layout-navbar">
      <van-nav-bar
        :title="title"
        left-text="返回"
        right-text="按钮"
        left-arrow
        @click-left="onClickLeft"
        @click-right="onClickRight"
      />
    </div>
    <div class="layout-content">
      <keep-alive v-if="$route.meta.keepAlive">
        <router-view></router-view>
      </keep-alive>
      <router-view v-else></router-view>
    </div>
    <div class="layout-footer">
      <TabBar :data="tabbars" @change="handleChange" />
    </div>
  </div>
</template>

<script>
import TabBar from '@/components/TabBar'
import { Toast } from 'vant'
export default {
  name: 'AppLayout',
  data() {
    return {
      title: '一张图',
      tabbars: [
        {
          title: '首页',
          to: {
            name: 'Home'
          },
          icon: 'home-o'
        },
        {
          title: '关于我',
          to: {
            name: 'About'
          },
          icon: 'user-o'
        },
        {
          title: '一张图',
          to: {
            name: 'Map'
          },
          icon: 'user-o'
        }
      ]
    }
  },
  components: {
    TabBar
  },
  watch: {
    $route: {
    handler: function(route) {
        this.title = route.meta && route.meta.title
      },
      immediate: true
    }
  },
  methods: {
    handleChange(v) {
      console.log('tab value:', v)
    },
    onClickLeft() {
      // Toast('返回')
      this.$router.go(-1)
    },
    onClickRight() {
      Toast('按钮')
    }
  }
}
</script>

<style lang="scss" scoped>
  .layout-content {
    height: calc(100% - 96px);
    width: 100%;
  }
</style>
