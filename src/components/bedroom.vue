<template>
  <div>
      <div id="bedroom">123</div>
  </div>
</template>

<script>
import echarts from 'echarts';
import data from '../../static/data/data.json'
export default {
    data(){
        return {
            chart:null
        }
    },
    methods:{
        drawPia(id){
            this.chart=echarts.init(document.getElementById(id));
            this.chart.setOption({
                tooltip:{
                    trigger:'item',
                    fformatte:"{b}: {c} ({d}%)"
                },
                legend:{
                    orient: 'vertical',
                    left: 5,
                    top: 10,
                    data:data.bedroom.opinion
                },
                series:[
                    {
                        name:'教室学习氛围',
                        type:'pie',
                        radius: ['50%', '70%'], //显示是否是圆形还是环形
                        avoidLabelOverlap: false,
                        label: {
                            //默认提示文字在环形内显示  如果不写 就显示在外围
                            // normal: {   
                            //     show: false,
                            //     position: 'center'
                            // },
                            emphasis: {
                                show: true,
                                textStyle: {
                                    fontSize: '30',
                                    fontWeight: 'bold'
                                }
                            }
                        },
                        //这个感觉没什么用
                        labelLine: {
                            normal: {
                                show: false
                            }
                        },
                        data:data.bedroom.opinionData,
                    }
                    
                ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('bedroom');
            var that=this;
            var resizeTimer = null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('bedroom')
                },100)
            }
        })
    }
}
</script>

<style>
#bedroom {
    position: relative;
    left: 50%;
    width: 90%;
    height: 600px;
    margin-left: -45%;
    border: solid #D01257 1px;
    box-shadow: 0 0 8px #FB90B7;
    border-radius: 10px;
  }   
  @media screen and (max-width: 470px) {
    #bedroom {
      height: 500px;
    }
  }
</style>
