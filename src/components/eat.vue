<template>
  <div>
      <div id="eat"></div>
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
                    text:'日常消费'
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
                    data:data.eat.money
                    }
                ],
                yAxis:[
                    {
                        type : 'value',
                        name:'人数',
                    }
                ],
                series:[
                    {
                        type:'bar',
                        //设置树状图顶部是否有没有数据
                        label: {
                                normal: {
                                show: true,
                                position: 'top'
                                }
                            },
                        data:data.eat.number,
                        markPoint : {
                            data : [
                                {type : 'max', name: '最大值'},
                                {type : 'min', name: '最小值'}
                            ]
                        },
                        markLine : {
                            data : [
                                {type : 'average', name: '平均值'}
                            ]
                        },
                         itemStyle: {
                            normal: {
                            barBorderRadius: 20,
                            color: 'yellowgreen',
                            shadowColor: 'rgba(0, 0, 0, 0.4)',
                            shadowBlur: 20,
                            
                            },
                        }
                    } 
                ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('eat')
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('eat');
                },100)
            }
        })
    }
}
</script>

<style>
#eat{
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
    #eat {
        height: 500px;
    }
  }
</style>
