<template>
  <div class="power">
    <h3>开启全部权限</h3>
    <el-switch v-model="value" active-color="#13ce66" inactive-color="#ff4949"></el-switch>
    <p>权限列表更新时间：{{ date }}</p>
  </div>
</template>
<script>
export default {
  name: 'power',
  data() {
    return {
      value: false,
      date: new Date().toLocaleDateString(),
    }
  },
}
</script>
<style></style>
