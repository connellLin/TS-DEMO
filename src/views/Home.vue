<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <searchBox @sendCity="sendCity" />
    <popularCity @popularCity="clickCity" />
    <weather :searchCity="city" :popularCity="city" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import searchBox from "@/components/searchBox.vue";
import popularCity from "@/components/popularCity.vue";
import weather from "@/components/weather.vue";

@Component({
  components: {
    searchBox,
    popularCity,
    weather,
  },
})
export default class Home extends Vue {
  city = "";

  sendCity(city: string): void {
    //搜索框组件向home组件传值
    this.city = city;
  }

  clickCity(city: string): void {
    //热门城市传值
    this.city = city;
  }
}
</script>

<style scoped lang="scss">
.home {
  width: 100%;
  height: 500px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
