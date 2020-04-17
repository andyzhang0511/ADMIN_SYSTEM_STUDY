<template>
  <!-- 如果你的路由是多级目录，如本项目 @/views/nested 那样，
有三级路由嵌套的情况下，不要忘记还要手动在二级目录的根文件下添加一个 <router-view> -->
  <div style="padding:30px;">
    <el-alert :closable="false" title="menu 1">
      <router-view />
    </el-alert>
  </div>
</template>
