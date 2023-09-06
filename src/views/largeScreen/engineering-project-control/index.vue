<template>
  <div class="engineering-project-control">
    <dv-full-screen-container>
        <div class="header">
          <dv-decoration-8 style="width:300px;height:70px;" />
          <dv-decoration-8 :reverse="true" style="width:300px;height:70px;" />
          <dv-decoration-5 style="width:1150px;height:60px;" />
          <div class="title">荆建分公司作业集约管控中心数字看板</div>
          <div class="dateTime"><span>{{date}}</span> <span style="margin: 0 10px;">{{week}}</span> <span>{{time}}</span></div>
        </div>
        <dv-border-box-1 class="content">
          <div class="content-left">
            <dv-border-box-8>
              <div class="title">合同管理情况</div>
              <ve-ring :data="chartData" :legend-visible="false" style="width:100%;"></ve-ring>
              <!-- <dv-loading>Loading...</dv-loading> -->
            </dv-border-box-8>
            <dv-border-box-8>
              <div class="title">施工承载情况</div>
              <!-- <dv-loading>Loading...</dv-loading> -->
            </dv-border-box-8>
            <dv-border-box-8>
              <div class="title">停电计划批复情况</div>
              <!-- <dv-loading>Loading...</dv-loading> -->
            </dv-border-box-8>
          </div>
          <div class="content-center">
            <dv-border-box-10>
              <ve-map :chart-data="mapData" :chart-settings="mapSettings" style="height: 100%;"></ve-map>
              <dv-loading>Loading...</dv-loading>
            </dv-border-box-10>
          </div>
          <div class="content-right">
            <dv-border-box-8 :reverse="true">
              <div class="title">施工工器具管理情况</div>
              <!-- <dv-loading>Loading...</dv-loading> -->
            </dv-border-box-8>
            <dv-border-box-8 :reverse="true">
              <div class="title">甲供物质到货情况</div>
              <!-- <dv-loading>Loading...</dv-loading> -->
            </dv-border-box-8>
            <dv-border-box-8 :reverse="true">
              <div class="title">作业文本审批情况</div>
              <!-- <dv-loading>Loading...</dv-loading> -->
            </dv-border-box-8>
          </div>
        </dv-border-box-1>
    </dv-full-screen-container>
  </div>
</template>

<script>
import { VeRing, VeMap } from 'v-charts'
import 'v-charts/lib/style.css';
import moment from 'moment'
export default {
  name: 'engineering-project-control',
  components: { VeRing, VeMap },
  mixins: [],
  computed: {},
  data() {
    return {
      date: '',
      week: '',
      time: '',
      interval: '',
      chartData: {
        hoverAnimation: true,
        radius: [ 80,  85 ],
        columns: ['类型', '合同数'],
        rows: [
          { '类型': '意向总包合同数', '合同数': 100 },
          { '类型': '已签订总包合同数', '合同数': 200 },
          { '类型': '意向分包合同数', '合同数': 345 },
          { '类型': '已签订分包合同数', '合同数': 300 },
        ]
      },
      mapData: [
        { name: '海门', value: 9 },
        { name: '莱芜', value: 148 },
        { name: '常德', value: 152 },
        { name: '保定', value: 153 },
        { name: '湘潭', value: 154 },
        { name: '金华', value: 157 },
        { name: '岳阳', value: 169 },
        { name: '长沙', value: 175 },
        { name: '衢州', value: 177 },
        { name: '廊坊', value: 193 },
        { name: '菏泽', value: 194 },
        { name: '合肥', value: 229 },
        { name: '武汉', value: 273 },
        { name: '大庆', value: 279 }
      ],
      mapSettings: {
        // 地图的配置选项
        mapURLProfix: 'https://unpkg.com/echarts@3.6.2/map/json/'
      },
    }
  },
  methods: {
    initDateTime() {
      const now = moment().locale('zh-cn');
      this.date = now.format('LL');
      this.week = now.format('dddd');
      this.time = now.format('HH:mm:ss');
    }
  },
  created() {
    setInterval(() => this.initDateTime(), 1000);
  },
  beforeDestroy() {
    clearInterval(this.interval);
  }
}
</script>

<style lang="scss">
.engineering-project-control{
  width: 100%;
  height: 100%;
  color: #fff;
  background-image: url(../../../assets/images/bg.png);
  background-size: 100% 100%;

  #dv-full-screen-container{
    display: flex;
    flex-direction: column;

    .header{
      width: 100%;
      height: 100px;
      position: relative;

      >.dv-decoration-8:nth-child(1),
      >.dv-decoration-8:nth-child(2){
        position: absolute;
        top: 0;
      }

      >.dv-decoration-8:nth-child(1){
        left: 0;
      }

      >.dv-decoration-8:nth-child(2){
        right: 0;
      }

      .dv-decoration-5{
        position: absolute;
        left: 50%;
        bottom: 0px;
        -webkit-transform: translateX(-50%);
        transform: translateX(-50%);
      }

      .title{
        position: absolute;
        font-size: 30px;
        font-weight: 700;
        left: 50%;
        top: 25px;
        -webkit-transform: translateX(-50%);
        transform: translateX(-50%);
      }

      .dateTime{
        position: absolute;
        font-size: 16px;
        top: 75px;
        right: 280px;
        font-weight: 700;
      }
    }
    
    .content{
      flex: 1;

      >.border-box-content{
        width: 100%;
        height: 100%;
        display: flex;
        padding: 20px;
        position: relative;
        
        .content-left,
        .content-right{
          flex: 0.6;
          display: flex;
          flex-direction: column;

          >.dv-border-box-8{
            flex: 1;
            
            >.border-box-content{
              display: flex;
              flex-direction: column;

              .title{
                height: 50px;
                line-height: 50px;
                font-size: 18px;
                font-weight: 700;
                padding-left: 20px;
              }
            }
          }

          >.dv-border-box-8:nth-child(2){
            margin: 10px 0;
          }
        }

        .content-center{
          flex: 1;
          margin: 0 10px;
        }
      }
    }
  }
}
</style>
