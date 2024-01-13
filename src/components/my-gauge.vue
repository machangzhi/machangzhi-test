<template>
  <div>
    <div id="chart" style="width: 600px; height: 400px"></div>
    <button @click="addValue">change</button>
  </div>
</template>

<script>
import * as echarts from "echarts"

export default {
  name: "MyGauge",
  data() {
    return {
      colors: [
        "#be535a",
        "#9e5c3e",
        "#aa953f",
        "#aaa348",
        "#8a9b29",
        "#709222",
      ],
      colorStops: [
        {
          offset: 0,
          color: "#be535a",
        },
        {
          offset: 0.2,
          color: "#9e5c3e",
        },
        {
          offset: 0.4,
          color: "#aa953f",
        },
        {
          offset: 0.6,
          color: "#aaa348",
        },
        {
          offset: 0.8,
          color: "#8a9b29",
        },
        {
          offset: 1,
          color: "#709222",
        },
      ],
      value: 10,
    }
  },
  mounted() {
    this.drowChart()
  },
  methods: {
    addValue() {
      if (this.value < 100) {
        this.value += 10
      } else {
        this.value = 10
      }

      this.drowChart()
    },
    drowChart() {
      if (this.value < 20) {
        this.colorStops = [
          {
            offset: 0,
            color: this.colors[0],
          },
          {
            offset: 1,
            color: this.colors[1],
          },
        ]
      } else if (this.value < 40) {
        this.colorStops = [
          {
            offset: 0,
            color: this.colors[0],
          },
          {
            offset: 0.5,
            color: this.colors[1],
          },
          {
            offset: 1,
            color: this.colors[2],
          },
        ]
      } else if (this.value < 60) {
        this.colorStops = [
          {
            offset: 0,
            color: this.colors[0],
          },
          {
            offset: 0.33,
            color: this.colors[1],
          },
          {
            offset: 0.66,
            color: this.colors[2],
          },
          {
            offset: 1,
            color: this.colors[3],
          },
        ]
      } else if (this.value < 80) {
        this.colorStops = [
          {
            offset: 0,
            color: this.colors[0],
          },
          {
            offset: 0.25,
            color: this.colors[1],
          },
          {
            offset: 0.5,
            color: this.colors[2],
          },
          {
            offset: 0.75,
            color: this.colors[3],
          },
          {
            offset: 1,
            color: this.colors[4],
          },
        ]
      } else {
        this.colorStops = [
          {
            offset: 0,
            color: this.colors[0],
          },
          {
            offset: 0.2,
            color: this.colors[1],
          },
          {
            offset: 0.4,
            color: this.colors[2],
          },
          {
            offset: 0.6,
            color: this.colors[3],
          },
          {
            offset: 0.8,
            color: this.colors[4],
          },
          {
            offset: 1,
            color: this.colors[5],
          },
        ]
      }
      let chartDom = document.getElementById("chart")
      // 初始化图表
      let myChart = echarts.init(chartDom)

      // 设置图表选项和数据
      let option = {
        series: [
          {
            type: "gauge", // 设置图表类型为仪表盘
            startAngle: 180, // 设置仪表盘的起始角度
            endAngle: 0, // 设置仪表盘的结束角度
            min: 0, // 设置仪表盘的最小值
            max: 100, // 设置仪表盘的最大值
            splitNumber: 1, // 设置仪表盘的分割段数
            itemStyle: {
              // 设置仪表盘的样式
              color: "#58D9F9", // 设置仪表盘的背景颜色
            },
            emphasis: {
              // 设置鼠标悬停时的样式
              disabled: true, // 设置鼠标悬停时是否禁用仪表盘
            },
            progress: {
              // 进度条
              show: true, // 设置进度条是否显示
              roundCap: true, // 设置进度条是否为圆角
              width: 18, // 设置进度条的宽度
              itemStyle: {
                color: {
                  type: "linear",
                  x: 0,
                  y: 1,
                  x2: 1,
                  y2: 1,
                  colorStops: this.colorStops,
                  global: false, // 缺省为 false
                },
              },
            },
            pointer: {
              // 指针
              show: false, // 设置指针是否显示
            },
            axisLine: {
              // 刻度线
              roundCap: true, // 设置刻度线的圆角
              lineStyle: {
                // 设置刻度线的样式
                width: 18, // 设置刻度线的宽度
              },
            },
            axisTick: {
              // 刻度
              splitNumber: 1, // 设置刻度的分割段数
              lineStyle: {
                // 设置刻度的样式
                width: 0, // 设置刻度线的宽度
              },
            },
            splitLine: {
              // 分隔线
              show: false, // 设置分隔线是否显示
            },
            axisLabel: {
              // 刻度标签
              distance: 5, // 设置刻度标签与刻度线的距离
              color: "#999", // 设置刻度标签的颜色
              fontSize: 15, // 设置刻度标签的字体大小
            },
            title: {
              // 标题
              show: false, // 设置标题是否显示
            },
            detail: {
              // 详情
              offsetCenter: [0, -25], // 设置详情的位置
              valueAnimation: true, // 设置详情的值是否进行动画
              formatter: function (value) {
                // 设置详情的格式
                return `{name|上次诊断得分}\n{value|${value.toFixed(
                  0
                )}}{unit|分}`
              },
              rich: {
                // 设置详情的富文本样式
                name: {
                  fontSize: 24,
                  color: "#000",
                  align: "center",
                  padding: [0, 0, 70, 0],
                },
                value: {
                  fontSize: 50,
                  color: "#000",
                  align: "center",
                  verticalAlign: "middle",
                },
                unit: {
                  fontSize: 20,
                  color: "#999",
                  align: "center",
                  verticalAlign: "bottom",
                  padding: [0, 0, 0, 5],
                },
              },
            },
            data: [
              {
                value: this.value,
              },
            ],
          },
        ],
      }

      // 将选项设置到图表中并渲染图表
      myChart.setOption(option)
    },
  },
}
</script>

<style scoped></style>
