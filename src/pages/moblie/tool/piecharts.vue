<template>
    <div class="piecharts" >
        <a ref="menu-wrapper1" style="width:100%;height:100%;display:block;"></a>
    </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'piecharts',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      gy: {},
      qyfb: []
    }
  },
  props:['radius','colors','data'],
  created () {
    var _this = this;
    var d = [];
    d.push({'value':this.data.syrs,'name':'已办理'})
    d.push({'value':this.data.wcrs,'name':'未办理'})
    this.$nextTick(function () {
      var i =0;
      // var colors=['#ceb5db','#ffb1b4'];
      var colors = this.colors; 
      var op = {
        tooltip: {
          trigger: 'item',
          position:function(p){   //其中p为当前鼠标的位置
            return [p[0] + 10, p[1] - 10];
        },
          formatter: ' {a} <br/>{b}: {c} ({d}%) '
        },
        series: [
          {
            name: '访问来源',
            type: 'pie',
            radius: this.radius,
            avoidLabelOverlap: false,
            center:['40%','40%'],
            hoverAnimation:false,
            itemStyle : {  
                      normal : {  
                          color:function(){  
                              return colors[i++];   
                              },  
                          label : {  
                              show : false  
                          },  
                          labelLine : {  
                              show : false  
                          }  
                      }
                  },  
            labelLine: {
              normal: {
                show: false
              }
            },
            data: d
          }
        ]
      }
      this.chart = echarts.init(this.$refs['menu-wrapper1'])
      this.chart.setOption(op)
    })
  },
  metheds: {
    createPie: function () {
      console.log(1)
      console.log(this.$refs['menu-wrapper1'])
    }
  }
}
</script>
<style scoped>
.piecharts{
  height:100%;
}
</style>
