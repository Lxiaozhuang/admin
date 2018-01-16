<template>
  <div>
      <div id="getup"></div>
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
                    text:'起床时间'
                },
                tooltip:{
                    trigger: 'axis'
                },
                
                toolbox: {
                    show : true,
                    feature : {
                        mark : {show: true},
                        dataView : {show: true, readOnly: false},
                        magicType : {show: true, type: ['line', 'bar']},
                        restore : {show: true},
                        saveAsImage : {show: true}
                    }
                },
                xAxis:[
                    {
                    type : 'category',
                    boundrayGap: false,
                    data:data.getup.time
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
                        name: '起床时间',
                        type:'bar',
                        //设置树状图顶部是否有没有数据
                        label: {
                                normal: {
                                show: true,
                                position: 'top'
                                }
                            },
                        data:data.getup.number,
                        markPoint : {
                            data : [
                                {type : 'max', name: '最大值'},
                                {type : 'min', name: '最小值'}
                            ]
                        },
                        
                    },
                    
                ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('getup');
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('getup');
                },100)
            }
        })
    }
}
</script>

<style>
#getup{
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
    #getup {
        height: 500px;
    }
  }
</style>
