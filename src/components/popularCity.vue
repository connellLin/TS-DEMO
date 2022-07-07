<template>
  <div id="city">
    <div v-for="(item, index) in message" :key="index">
      <el-button class="box-city" type="text" @click="clickCity(item)">
        {{item}}</el-button>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Emit } from "vue-property-decorator";

@Component({
  components: {},
})
export default class searchBox extends Vue {
  message = ["北京", "上海", "深圳", "成都", "重庆", "武汉", "南京"];

  @Emit("popularCity")
  clickCity(city: string): string {
    console.log("点击热门城市：" + city);
    return city;
  }
}
</script>

<style lang="scss" scoped>
@import "../style/index.scss";
#city {
  width: 40%;
  @include box-row-flex(center);

  .box-city {
    width: 10%;
    // font-style: italic;
    color: $text-color;
    font-size: $font-size;
  }
}
</style>
