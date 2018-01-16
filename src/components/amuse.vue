<template>
  <div>
      <div id="amuse"></div>
  </div>
</template>

<script>
import echarts from 'echarts';
import data from '../../static/data/data.json'
export default {
    data(){
        return {
            chart:null,
            
        }
    },
    methods:{
        drawPia(id){
            this.chart=echarts.init(document.getElementById(id));
            var dataStyle = {
                normal: {
                    label: {show:false},
                    labelLine: {show:false}
                }
            };
            var placeHolderStyle = {
                normal : {
                    color: 'rgba(0,0,0,0)',
                    label: {show:false},
                    labelLine: {show:false}
                },
                emphasis : {
                    color: 'rgba(0,0,0,0)'
                }
            };
            this.chart.setOption({
                tooltip : {
                show: true,
                formatter: "{a} <br/>{b} : {c} ({d}%)"
            },
            legend: {
                orient : 'vertical',
                x : 10,
                y : 35,
                itemGap:12,
                data:data.amuse.amuse
            },
            toolbox: {
                show : true,
                feature : {
                    mark : {show: true},
                    dataView : {show: true, readOnly: false},
                    restore : {show: true},
                    saveAsImage : {show: true}
                }
            },
            series : [
                {
                    name:data.amuse.amuseData[0].name,
                    type:'pie',
                    clockWise:false,
                    radius : [220, 240],
                    itemStyle : dataStyle,
                    data:[
                        data.amuse.amuseData[0],
                        {
                            value:4,
                            name:'invisible',
                            itemStyle : placeHolderStyle
                        }
                    ]
                },
                {
                    name:data.amuse.amuseData[1].name,
                    type:'pie',
                    clockWise:false,
                    radius : [200, 220],
                    itemStyle : dataStyle,
                    data:[
                        data.amuse.amuseData[1],
                        
                        {
                            value:14,
                            name:'invisible',
                            itemStyle : placeHolderStyle
                        }
                    ]
                },
                {
                    name:data.amuse.amuseData[2].name,
                    type:'pie',
                    clockWise:false,
                    radius : [180, 200],
                    itemStyle : dataStyle,
                    data:[
                        data.amuse.amuseData[2],
                        
                        {
                            value:18,
                            name:'invisible',
                            itemStyle : placeHolderStyle
                        }
                    ]
                },
                {
                    name:data.amuse.amuseData[3].name,
                    type:'pie',
                    clockWise:false,
                    radius : [160, 180],
                    itemStyle : dataStyle,
                    data:[
                        data.amuse.amuseData[3],
                        
                        {
                            value:20,
                            name:'invisible',
                            itemStyle : placeHolderStyle
                        }
                    ]
                },
                {
                    name:data.amuse.amuseData[4].name,
                    type:'pie',
                    clockWise:false,
                    radius : [140, 160],
                    itemStyle : dataStyle,
                    data:[
                        data.amuse.amuseData[4],
                        
                        {
                            value:28,
                            name:'invisible',
                            itemStyle : placeHolderStyle
                        }
                    ]
                },
                {
                    name:data.amuse.amuseData[5].name,
                    type:'pie',
                    clockWise:false,
                    radius : [120, 140],
                    itemStyle : dataStyle,
                    data:[
                        data.amuse.amuseData[5],
                        
                        {
                            value:28,
                            name:'invisible',
                            itemStyle : placeHolderStyle
                        }
                    ]
                },
            ]
            })
        }
    },
    mounted(){
        this.$nextTick(function(){
            this.drawPia('amuse')
            var that=this;
            var resizeTimer=null;
            window.onresize=function(){
                if(resizeTimer) clearTimeout(resizeTimer);
                resizeTimer=setTimeout(function(){
                    that.drawPia('amuse')
                },100)
            }
        })
    }
}
</script>

<style>
#amuse {
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
    #amuse {
      height: 500px;
    }
  }
</style>
