<template>
  <div>
      <div id="gotobed"></div>
  </div>
</template>

<script>
import echarts from 'echarts';
import data from '../../static/data/data.json';
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
                title:{
                    text:'睡觉时间',
                },
                tooltip:{
                    trigger:'axis'
                },
                toolbox: {
                    show : true,
                    feature : {
                        magicType : {show: true, type: ['line', 'bar']},
                        restore : {show: true},
                        saveAsImage : {show: true}
                    }
                },
                xAxis:[
                    {
                    type : 'category',
                    boundrayGap: false,
                    data:data.gotobed.time
                }
                ],
                yAxis:[
                    {
                        type : 'value',
                        name:'人数',
                    }
                ],
                series : [
                    {
                        type:'bar',
                        //设置树状图顶部是否有没有数据
                        label: {
                                normal: {
                                show: true,
                                position: 'top'
                                }
                            },
                        data:data.gotobed.number,
                        itemStyle: {
                            normal: {
                            barBorderRadius: 20,
                            color: 'purple',
                            shadowColor: 'rgba(0, 0, 0, 0.4)',
                            shadowBlur: 20,
                            areaStyle: {
                                color: 'purple',
                                type: 'default',
                                },
                            }
                        },
                        
                    },
                ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('gotobed');
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('gotobed');
                },100)
            }
        })
    }
}
</script>

<style>
#gotobed{
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
    #gotobed {
        height: 500px;
    }
  }
</style>
