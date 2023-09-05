<template>
  <div class="home">
    <dv-full-screen-container>
      <dv-border-box-1>
        <div class="header">
          <!-- <dv-decoration-8 style="width:480px;height:60px;" /> -->
          <!-- <dv-decoration-8 :reverse="true" style="width:480px;height:60px;" /> -->
          <dv-decoration-5 style="width:768px;height:60px;" />
          <div class="title">智能大屏展示系统</div>
        </div>
        <div class="content"></div>
      </dv-border-box-1>
    </dv-full-screen-container>
  </div>
</template>

<script>
export default {
  name: 'Layout',
  components: {},
  mixins: [],
  computed: {},
  methods: {}
}
</script>

<style lang="scss">
.home{
  width: 100%;
  height: 100%;
  background-color: #030409;
  color: #fff;

  .border-box-content{
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
        top: 30px;
        -webkit-transform: translateX(-50%);
        transform: translateX(-50%);
      }

      .title{
        position: absolute;
        font-size: 30px;
        font-weight: 700;
        left: 50%;
        top: 15px;
        -webkit-transform: translateX(-50%);
        transform: translateX(-50%);
      }
    }

    .content{
      width: 100%;
      flex: 1;
    }
  }
}
</style>
