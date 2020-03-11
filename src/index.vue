<template>
  <div class="component"></div>
</template>

<script>
  import {VueExtend, Util} from 'godspen-lib'

  export default {
    mixins: [VueExtend.mixin],
    name: 'echarts',
    label: process.env.LABEL,
    style: process.env.STYLE,
    stack: false, // 是否是堆叠模式 ，true：孩子元素会按楼层一个个向下排布， false: 孩子元素绝对定位，随意放置位置
    childLimit: 9999,  // 孩子元素最大限制数
    leaf: false, // 是否是叶子节点，为true的时候该节点下面不能添加节点
    props: {
      reanderType: {
        type: String,
        default: 'canvas',
        editor: {
          type: 'Object',
          label: '配置信息',
          desc: 'echarts的option配置信息'
        },
      },
      // 文本框输入
      option: {
        type: [Object],
        editor: {
          type: 'Object',
          label: '配置信息',
          desc: 'echarts的option配置信息'
        },
        default () {
          return {
            title: {
              text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
              data: ['销量']
            },
            xAxis: {
              data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
            },
            yAxis: {},
            series: [{
              name: '销量',
              type: 'bar',
              data: [5, 20, 36, 10, 10, 20]
            }]
          }
        }
      },
    },
    computed: {
    },
    mounted: async function () {
      this.echartType = typeof window.echarts
      // 纯属演示异步加载js资源，与本组件无关； loadJs返回一个promise实例 可以用async 或者 then 来处理回调
      await Util.loadJs('https://cdn.bootcss.com/echarts/4.6.0/echarts.min.js')
      this.echartType = typeof window.echarts
      var myChart = window.echarts.init(this.$el)
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(this.option)
    },
    editorMethods: {
    },
    methods: {
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component {
    width: 100%;
    height: 100%;
  }
</style>
