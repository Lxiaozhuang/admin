<template>
  <div>
      <div id="single"></div>
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
                title : {
                text: '是否单身',
                x:'center'
            },
            tooltip : {
                trigger: 'item',
                formatter: "{a} <br/>{b} : {c} ({d}%)"
            },
            legend: {
                orient: 'vertical',     //文字垂直排序
                top:10,
                left:5,
                data:data.single.course
            },
            toolbox: {
                show : true,
                feature : {
                    mark : {show: true},
                    dataView : {show: true, readOnly: false},
                    magicType : {
                        show: true, 
                        type: ['pie', 'funnel']
                    },
                    restore : {show: true},
                    saveAsImage : {show: true}
                }
            },
            calculable : true,
            series : [
                {
                    name:'半径模式',
                    type:'pie',
                    radius : [80, 170],
                    center : ['50%', 300],
                    roseType : 'radius',
                    width: '40%',       // for funnel
                    max: 40,            // for funnel
                    itemStyle : {
                        normal : {
                            label : {
                                show : false
                            },
                            labelLine : {
                                show : false
                            }
                        },
                        emphasis : {
                            label : {
                                show : true
                            },
                            labelLine : {
                                show : true
                            }
                        }
                    },
                    data:data.single.courseDiff
                },
               ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('single');
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('single');
                },100)
            }
        })
    }
}
</script>

<style>
 #single{
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
    #single {
        height: 500px;
    }
  }
</style>
