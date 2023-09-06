<template>
  <div class="job-risk-control">
    <dv-full-screen-container>
        <div class="header">
          <dv-decoration-8 style="width:300px;height:70px;" />
          <dv-decoration-8 :reverse="true" style="width:300px;height:70px;" />
          <dv-decoration-5 style="width:1150px;height:60px;" />
          <div class="title">荆建分公司作业集约管控中心数字看板</div>
          <div class="dateTime"><span>{{date}}</span> <span style="margin: 0 10px;">{{week}}</span> <span>{{time}}</span></div>
        </div>
        <div class="content">
          <dv-border-box-1>
            <div class="content-left">
              <dv-border-box-8><dv-loading>Loading...</dv-loading></dv-border-box-8>
              <dv-border-box-8><dv-loading>Loading...</dv-loading></dv-border-box-8>
              <dv-border-box-8><dv-loading>Loading...</dv-loading></dv-border-box-8>
            </div>
            <div class="content-center"><dv-border-box-10><dv-loading>Loading...</dv-loading></dv-border-box-10></div>
            <div class="content-right">
              <dv-border-box-8 :reverse="true"><dv-loading>Loading...</dv-loading></dv-border-box-8>
              <dv-border-box-8 :reverse="true"><dv-loading>Loading...</dv-loading></dv-border-box-8>
              <dv-border-box-8 :reverse="true"><dv-loading>Loading...</dv-loading></dv-border-box-8>
            </div>
          </dv-border-box-1>
        </div>
    </dv-full-screen-container>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'job-risk-control',
  components: {},
  mixins: [],
  computed: {},
  data() {
    return {
      date: '',
      week: '',
      time: '',
      interval: '',
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
.job-risk-control{
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

      .border-box-content{
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

          >div{
            flex: 1;
          }

          >div:nth-child(2){
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
