<template>
  <div>
      <div id="interestpie"></div>
  </div>
</template>

<script>
import echarts from "echarts";
import data from '../../static/data/data.json'
export default {
      data(){
          return {
              chart:null
          }
      },
      methods:{
          drawPia(id,small,big){
              this.chart=echarts.init(document.getElementById(id));
              this.chart.setOption({
                tooltip : {
                    trigger: 'item',
                    formatter: "{a} <br/>{b} : {c} ({d}%)"
                },
                legend: {   //调整左侧显示文字的位置
                     orient: 'vertical',    
                    left: 5,
                    top: 10,
                    data:data.interest.course
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
                        name:'课程兴趣调查',
                        type:'pie', 
                        radius : [small, big],
                        center : ['50%', '60%'],    //调整图形的位置
                        roseType : 'area',
                        data:data.interest.courseInter
                    }
                ]
            })
        }
      },
      mounted(){
          this.$nextTick(function(){
              if(document.body.clientWidth<560){
                  this.drawPia('interestpie',30,100)
              }else{
                  this.drawPia('interestpie',60,240)
              }
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    if(document.body.clientWidth<560){
                        this.drawPia('interestpie',30,100)
                    }else{
                        this.drawPia('interestpie',60,240) 
                    }
                },100)
            }
        })
      }

}   
</script>

<style>
    #interestpie{
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
    #interestpie {
        height: 500px;
    }
  }
</style>
