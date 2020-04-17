<template>
  <!-- 这里在 app-main 外部包了一层 keep-alive 主要是为了缓存 <router-view> 的，
配合页面的 tabs-view 标签导航使用，如不需要可自行去除。
其中transition 定义了页面之间切换动画，可以根据自己的需求，自行修改转场动画。相关文档。
默认提供了fade和fade-transform两个转场动画，具体 css 实现见transition.scss。如果需要调整可在AppMain.vue中调整transition 的 name。 -->
  <section class="app-main">
    <transition name="fade-transform" mode="out-in">
      <keep-alive :include="cachedViews">
        <!-- 加上一个唯一的 key，来保证路由切换时都会重新渲染触发钩子 -->
        <router-view :key="key" />
      </keep-alive>
    </transition>
  </section>
</template>

<script>
export default {
  name: 'AppMain',
  computed: {
    cachedViews() {
      return this.$store.state.tagsView.cachedViews
    },
    // 只要保证 key 唯一性就可以了，保证不同页面的 key 不相同
    key() {
      return this.$route.path
    }
  }
}
</script>

<style lang="scss" scoped>
.app-main {
  /* 50= navbar  50  */
  min-height: calc(100vh - 50px);
  width: 100%;
  position: relative;
  overflow: hidden;
}

.fixed-header+.app-main {
  padding-top: 50px;
}

.hasTagsView {
  .app-main {
    /* 84 = navbar + tags-view = 50 + 34 */
    min-height: calc(100vh - 84px);
  }

  .fixed-header+.app-main {
    padding-top: 84px;
  }
}
</style>

<style lang="scss">
// fix css style bug in open el-dialog
.el-popup-parent--hidden {
  .fixed-header {
    padding-right: 15px;
  }
}
</style>
