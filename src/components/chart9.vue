<template>
  <div class="图3">
    <h3>犯罪年龄趋势图</h3>
    <div ref="divRef" class="chart"></div>
  </div>

</template>

<script>
import {onMounted, ref} from "vue";
import * as echarts from "echarts";
import {px} from "../assets/px.js";
import {createEchartsOptions} from "../assets/create-echarts-options.js";

export default {
  setup() {
    const divRef = ref(null);
    onMounted(() => {
      const myChart = echarts.init(divRef.value)
      myChart.setOption(createEchartsOptions({

        color: '#F7A110',
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: [0, 18, 28, 38, 48, 58, 68, 78],
          splitLine: {show: true, lineStyle: {color: '#073E78'}},
          axisTick: {show: false},
          axisLine: {show: false},
        },
        yAxis: {
          type: 'value',
          splitLine: {lineStyle: {color: '#073E78'}},
          axisLabel: {
            formatter(val) {
              return val * 100 + '%';
            }
          }
        },
        series: [{
          type: 'line',
          data: [
            0, 0.20, 0.26,
            0.35, 0.26, 0.20,
            0.08, 0.06
          ],
          symbol: 'circle',
          symbolSize: px(12),
          lineStyle: {width: px(2)},
          areaStyle: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
              offset: 0,
              color: '#F7A110'
            }, {
              offset: 1,
              color: '#1B1D52'
            }]),
          }
        }]

      }))

      setInterval(()=>{
        myChart.clear()
        myChart.setOption(createEchartsOptions({

          color: '#F7A110',
          xAxis: {
            type: 'category',
            boundaryGap: false,
            data: [0, 18, 28, 38, 48, 58, 68, 78],
            splitLine: {show: true, lineStyle: {color: '#073E78'}},
            axisTick: {show: false},
            axisLine: {show: false},
          },
          yAxis: {
            type: 'value',
            splitLine: {lineStyle: {color: '#073E78'}},
            axisLabel: {
              formatter(val) {
                return val * 100 + '%';
              }
            }
          },
          series: [{
            type: 'line',
            data: [
              0, 0.20, 0.26,
              0.35, 0.26, 0.20,
              0.08, 0.06
            ],
            symbol: 'circle',
            symbolSize: px(12),
            lineStyle: {width: px(2)},
            areaStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                offset: 0,
                color: '#F7A110'
              }, {
                offset: 1,
                color: '#1B1D52'
              }]),
            }
          }]

        }))
      },3000)

    })
    return {divRef}
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/css.scss";

.图3 {
  //border: 1px solid #08397d;
  h3 {
    font-size: 20/ 2420 * 100rem;
    color: #7ab6db;
    margin-top: 6/ 2420 * 100rem;
  }
  .chart {
    flex: 1;
    width: 100%;
  }
}
</style>
