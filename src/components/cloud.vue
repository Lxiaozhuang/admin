<template>
  <div>
      <div id="cloud"></div>
  </div>
</template>
<script>
import echarts from 'echarts';
import 'echarts-wordcloud';
import data from '../../static/data/data.json'
export default {
    data(){
        return  {
            chart:null
        }
    },
    methods:{
        drawPia(id){
            this.chart=echarts.init(document.getElementById(id));
            this.chart.setOption({
                tooltip: {
                show: true
                },
                series: [{
                    name: '妙味关键字',
                    type: 'wordCloud',
                    size: ['80%', '80%'],
                    textRotation : [0, 45, 90, -45],
                    textPadding: 0,
                    autoSize: {
                        enable: true,
                        minSize: 16
                    },
                    data:data.cloud.wordContent,
                    textStyle: {
                        normal: {
                            fontFamily: 'Microsoft Yahei',
                            fontWeight: 'bold',
                            color: function() {
                            return 'rgb(' + [
                                Math.round(Math.random() * 160),
                                Math.round(Math.random() * 160),
                                Math.round(Math.random() * 160)
                            ].join(',') + ')'
                            }
                        },
                        emphasis: {
                            shadowBlur: 10,
                            shadowColor: '#333'
                        }
                    },
                }]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('cloud');
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('cloud');
                },100)
            }
        })
    }
}
</script>

<style>
#cloud{
        position: relative;
        left: 50%;
        width: 90%;
        height: 620px;
        margin-left: -45%;
        border: solid #00AD7C 1px;
        box-shadow: 0 0 8px #52D681;
        border-radius: 10px;
    }   
    
    @media screen and (max-width: 560px) {
    #cloud {
        height: 500px;
    }
  }
</style>
