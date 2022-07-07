<template>
  <div id="search">
    <el-input
      placeholder="请输入内容"
      suffix-icon="el-icon-search"
      v-model="city"
      @change="enter"
      @input="edit"
    >
    </el-input>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Emit } from "vue-property-decorator";

@Component({
  components: {},
})
export default class searchBox extends Vue {
  city = "";

  @Emit("sendCity")
  enter(value: string): string {
    //在输入框失去焦点或用户按下回车时触发（会导致一些bug！！！）
    console.log("按下回车，搜索地是：" + value);
    return value;
  }

  edit(value: string | number): void {
    console.log("正在输入中......" + value);
  }
}
</script>
