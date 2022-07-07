<template>
  <div id="weather">
    <div v-for="(item, index) in weatherArr" :key="index">
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>{{ city }}</span>
        </div>
        <div class="content">
          <div class="type">{{ item.type }}</div>
          <div class="temp">
            {{ item.low | temperatureFilter }} ~
            {{ item.high | temperatureFilter }}
          </div>
          <div class="time">{{ item.date }}</div>
        </div>
      </el-card>
    </div>
  </div>
</template>

<script lang="ts">
import weather from "../interface/IWeather";
import getWeather from "../utils/getWeather";
import { Vue, Component, Prop, Watch } from "vue-property-decorator";

@Component({
  components: {},
  filters: {
    temperatureFilter: (value: string): string => {
      return value.substring(2);
    },
  },
})
export default class searchBox extends Vue {
  @Prop({
    type: String,
    default: "",
  })
  searchCity!: string;

  city = "深圳";
  weatherArr: Array<weather> = [];

  @Watch("searchCity")
  async handleWatch(value: string): Promise<void> {
    console.log("搜索框或热门城市传入的地区是：" + value);

    const res = await getWeather(value);
    console.log(res);
    if (res.status == 1000) {
      this.city = value;
      this.weatherArr.length = 0; //清空当前数组存入的数据
      this.weatherArr.push(...res.weather);
    } else if (res.status == 1002) {
      this.$message({
        message: res.desc as string,
        type: "error",
      });
    }
  }

  async created(): Promise<void> {
    const res = await getWeather(this.city);
    if (res.status == 1000) {
      this.weatherArr.push(...res.weather);
    } else if (res.status == 1002) {
      this.$message({
        message: res.desc as string,
        type: "error",
      });
    }
    console.log(res);
  }
}
</script>

<style lang="scss" scoped>
@import "../style/index.scss";
#weather {
  width: 100%;
  height: 200px;
  @include box-row-flex(space-around);

  .box-card {
    width: 15vw;
    height: 180px;

    .clearfix {
      height: 10px;
    }
    .clearfix:before,
    .clearfix:after {
      display: table;
      content: "";
    }
    .clearfix:after {
      clear: both;
    }

    .content {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      align-items: center;
      text-align: center;

      .type {
        width: 10vw;
        height: 40px;
        line-height: 40px;
        color: skyblue;
        font-size: 20px;
      }

      .temp,
      .time {
        height: 40px;
        line-height: 40px;
        font-size: 13px;
      }
    }
  }
}
</style>
