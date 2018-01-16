<template>
  <div>
      <div id="graduate"></div>
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
                title : {
                    text: '毕业展望',
                    x:'center'
                },
                tooltip : {
                    trigger: 'item',
                    formatter: "{a} <br/>{b} : {c} ({d}%)"
                },
                legend: {
                    orient : 'vertical',
                    x : 'left',
                    data:data.graduate.opinion
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
                        name:'人数',
                        type:'pie',
                        radius : '55%',
                        center: ['50%', '60%'],
                        data:data.graduate.opinionData
                    }
                ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('graduate');
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('graduate');
                },100)
            }
        })
    }


}
</script>

<style>
    #graduate{
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
    #graduate {
        height: 500px;
    }
  }
</style>
