<!--
 * @Description: 
 * @Author: lanchao
 * @Date: 2022-05-20 15:42:12
 * @LastEditTime: 2022-05-25 15:01:19
 * @LastEditors: lanchao
 * @Reference: 
-->
<template>
  <div class="label">{{ name }}</div>
  <div class="header">
    <el-icon @click="semiWin"><SemiSelect /></el-icon>
    <el-icon v-if="isMax" @click="fullWin"><FullScreen /></el-icon>
    <el-icon v-if="!isMax" @click="noFullWin"><CopyDocument /></el-icon>
    <el-icon @click="closeWin"><Close /></el-icon>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
@Options({
  props: {
    name: String
  }
})
export default class HeaderComponent extends Vue {
  isMax = false //是否最大化
  name = '' //视频标题
  closeWin = () => {
    ;(window as any).ipcRenderer.send('app-close')
  }
  semiWin = () => {
    ;(window as any).ipcRenderer.send('app-min')
  }
  fullWin = () => {
    this.isMax = false
    ;(window as any).ipcRenderer.send('app-max')
  }
  noFullWin = () => {
    this.isMax = true
    ;(window as any).ipcRenderer.send('app-max')
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.label {
  margin-left: auto;
  font-size: 25px;
  font-weight: bold;
  color: blue;
}
.header {
  -webkit-app-region: no-drag;
  display: flex;
  justify-content: space-between;
  width: 60px;
  margin-left: auto;
  cursor: pointer;
}
</style>
