<template>
  <div>
      <div id="difficult"></div>
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
                text: '课程难度调查',
                x:'center'
            },
            tooltip : {
                trigger: 'item',
                formatter: "{a} <br/>{b} : {c} ({d}%)"
            },
            legend: {
                orient : 'vertical',
                x : 'left',
                data:data.difficult.course
            },
            toolbox: {
                show : true,
                feature : {
                    mark : {show: true},
                    dataView : {show: true, readOnly: false},
                    magicType : {
                        show: true, 
                        type: ['pie', 'funnel'],
                        option: {
                            funnel: {
                                x: '25%',
                                width: '50%',
                                funnelAlign: 'left',
                                max: 1548
                            }
                        }
                    },
                    restore : {show: true},
                    saveAsImage : {show: true}
                }
            },
            calculable : true,
            series : [
                {
                    name:'访问来源',
                    type:'pie',
                    radius : '55%',
                    center: ['50%', '60%'],
                    data:data.difficult.courseDiff
                }
            ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('difficult');
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('difficult')
                },100)
            }
        })
    }
}
</script>

<style>
#difficult {
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
    #difficult {
      height: 500px;
    }
  }
</style>
