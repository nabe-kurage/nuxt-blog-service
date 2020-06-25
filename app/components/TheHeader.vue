<template>
  <el-menu>
    <el-menu-item index="1" >
      Nuxt Diary App
    </el-menu-item>
    <el-menu-item index="2" :route="{ path: '/posts/'}">
      新規一覧
    </el-menu-item>

    <no-ssr>
      <el-menu-item index="4" :route="{ path: '/posts/'}" v-if='user'>
        <span>ログイン中</span>
      </el-menu-item>
      <el-menu-item index="4" :route="{ path: '/posts/'}" v-else>
        <span>ログイン</span>
      </el-menu-item>
    </no-ssr>
    <el-menu-item index="5" :route="{ path: '/posts/new'}">
      新規投稿
    </el-menu-item>
  </el-menu>
</template>
˜
