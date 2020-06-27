<template>
  <section class="container post-page">
    <el-card>
      <div slot="header">
        <span>新規投稿</span>
      </div>
    </el-card>
  </section>
</template>

<script>
import { mapGetters, mapActions } from 'Vuex'
export default {
  computed: {
    ...mapGetters(['count'])
  },
  methods: {
    ...mapActions(['increment'])
  }

}
</script>

<style>

</style>
