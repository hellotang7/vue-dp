<template>
  <div ref="divRef" class="chart"></div>

</template>

<script>
import {onMounted, ref} from "vue";
import * as echarts from "echarts";
import {createEchartsOptions} from "../assets/create-echarts-options.js";
import {px} from "../assets/px.js";

export default {
  setup() {
    const divRef = ref(null);
    const data = [
      {value: 0.08, name: '浙江省'},
      {value: 0.06, name: '安徽省'},
      {value: 0.11, name: '江苏省'},
      {value: 0.09, name: '山东省'},
      {value: 0.12, name: '河南省'},
      {value: 0.06, name: '陕西省'},
      {value: 0.08, name: '河北省'},
      {value: 0.08, name: '云南省'},
      {value: 0.08, name: '贵州省'},
    ];
    onMounted(() => {
      const myChart = echarts.init(divRef.value)
      myChart.setOption(createEchartsOptions({

        xAxis: {
          data: data.map(i=>i.name),
          axisTick: {show: false},
          axisLine: {
            lineStyle: {color: '#083B70'}
          },
          axisLabel: {
            formatter(val) {
              if (val.length > 2) {
                const array = val.split('');
                array.splice(2, 0, '\n');
                return array.join('');
              } else {
                return val;
              }
            }
          },
        },

        yAxis: {
          splitLine: {show: false},
          axisLine: {
            show: true,
            lineStyle: {color: '#083B70'}
          },
          axisLabel: {
            formatter(value) {
              return (value * 100).toFixed(0) + '%';
            }
          }
        },
        series: [{
          type: 'bar',
          data: data.map(i=>i.value),
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
            offset: 0,
            color: '#0A97FB'
          }, {
            offset: 1,
            color: '#1E34FA'
          }]),
        }]

      }))

      setInterval(()=>{
        myChart.clear()
        myChart.setOption(createEchartsOptions({

          xAxis: {
            data: data.map(i=>i.name),
            axisTick: {show: false},
            axisLine: {
              lineStyle: {color: '#083B70'}
            },
            axisLabel: {
              formatter(val) {
                if (val.length > 2) {
                  const array = val.split('');
                  array.splice(2, 0, '\n');
                  return array.join('');
                } else {
                  return val;
                }
              }
            },
          },

          yAxis: {
            splitLine: {show: false},
            axisLine: {
              show: true,
              lineStyle: {color: '#083B70'}
            },
            axisLabel: {
              formatter(value) {
                return (value * 100).toFixed(0) + '%';
              }
            }
          },
          series: [{
            type: 'bar',
            data: data.map(i=>i.value),
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
              offset: 0,
              color: '#0A97FB'
            }, {
              offset: 1,
              color: '#1E34FA'
            }]),
          }]

        }))
      },3000)

    })
    return {divRef}
  }
}
</script>

<style lang="scss" scoped>
.chart {
  display: flex;
  flex: 1;
}
</style>
