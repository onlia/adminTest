<template>
  <div>
    <div ref="dom1" style="width: 600px;height: 400px;"></div>
    <div ref="dom2" style="width: 600px;height: 400px;"></div>
  </div>
</template>

<script>
import echarts from 'echarts'
import tdTheme from '_c/charts/theme.json'
import { on, off } from '@/libs/tools'
echarts.registerTheme('tdTheme', tdTheme) // 主题注册名
export default {
  mounted () {
    this.$nextTick(() => {
      this.cpu()
      this.server()
      on(window, 'resize', this.resize)
    })
  },
  methods: {
    resize () {
      this.dom1.resize()
      this.dom2.server()
    },
    cpu () {
      let option = {
        color: ['#FA5075'],
        xAxis: {
          type: 'category',
          boundaryGap: false,
          axisLabel: {
            interval: 0
          },
          data: ['16:00:00', '16:01:00', '16:02:00', '16:03:00', '16:04:00']
        },
        yAxis: {
          type: 'value',
          name: '       CPUUtilization(%)'
        },
        series: [{
          data: [10, 20, 15, 23, 30],
          type: 'line'
        }]
      }
      this.dom1 = echarts.init(this.$refs.dom1, 'tdTheme')
      this.dom1.setOption(option)
    },
    server () {
      let option = {
        color: ['#FA5075'],
        xAxis: {
          type: 'category',
          // boundaryGap: false,
          axisLabel: {
            interval: 0
          },
          data: ['one', 'two', 'three', 'four', 'five']
        },
        yAxis: {
          type: 'value',
          name: '       CPUUtilization(%)'
        },
        series: [{
          data: [10, 20, 15, 23, 30],
          type: 'pie',
          barWidth: '40%'
        }]
      }
      this.dom2 = echarts.init(this.$refs.dom2, 'tdTheme')
      this.dom2.setOption(option)
    }
  },
  beforeDestroy () {
    off(window, 'resize', this.resize)
  }
}
</script>
