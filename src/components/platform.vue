<template>
  <div class="platform">
    <p class="title">平台列表</p>
    <el-radio-group v-model="currentPlatform">
      <el-radio v-for="item in platformList" :key="item.key" :label="item.key">{{ item.name }}</el-radio>
    </el-radio-group>
  </div>
</template>
<script>
const platformList = [
  { name: '四格', key: 'segi' },
  { name: '招商', key: 'cmhk' },
  { name: '美的', key: 'midea' },
  { name: '永升', key: 'pms' },
  { name: '新大正', key: 'xdzxy' },
  { name: '鲁能', key: 'Inwy' },
  { name: '华润', key: 'crlano' },
  { name: '印力', key: 'scpg' },
  { name: '明喆', key: 'mzzf' },
  { name: '三一', key: 'sany' },
  { name: '开元', key: 'kywy' },
  { name: '合生活', key: 'hillife' },
  { name: '空港', key: 'kgw' },
  { name: '迅杨', key: 'nnh' },
  { name: '中外运', key: 'csc' },
  { name: '中电', key: 'cesz' },
  { name: '中海', key: 'copm' },
  { name: '太平', key: 'tpim' },
  { name: '宝丰', key: 'bfjt' },
  { name: '高地', key: 'goltebk' },
  { name: '越秀食品', key: 'yxsp' },
  { name: '华侨城', key: 'oct' },
]
export default {
  name: 'platform',
  data() {
    return {
      platformList,
      currentPlatform: 'segi',
    }
  },
}
</script>
<style>
.title {
  text-align: center;
}
</style>
