<template>
  <div class="box">
    <HeaderTop></HeaderTop>
    <div class="content">
      <tool ref="tool" @getLastCount="$refs.list.getLastCount()" @search="search" @delete="$refs.list.deleteRows()"
            @add="$refs.list.add()"></tool>
      <el-row :gutter="20" style="margin-top: 18px">
        <el-col :span="16">
          <home-list @changeDate="(date)=>{$refs.tool.setDate(date)}" @search="search" ref="list"></home-list>
        </el-col>
        <el-col :span="8">
          <el-tabs v-model="tabNow" @tab-click="tabClick" class="chartBox">
            <el-tab-pane name="total" label="总消费">
              <echart1 ref="echart1"></echart1>
              <echart2 ref="echart2" :params="params"></echart2>
            </el-tab-pane>
            <el-tab-pane name="vs" label="消费对比">
              <echart3 ref="echart3" @balance="search(params)"></echart3>
            </el-tab-pane>
          </el-tabs>
        </el-col>
      </el-row>
    </div>
  </div>

</template>

<script>
  import HomeList from "../components/homeList"
  import HeaderTop from "../components/headerTop"
  import Tool from "../components/tool"
  import Echart1 from "../components/echart1"
  import Echart2 from "../components/echart2"
  import Echart3 from "../components/echart3"

  export default {
    name: "home",
    data() {
      return {
        tabNow: "total",
        params: {}
      }
    },
    components: {Echart3, Echart1, Echart2, Tool, HeaderTop, HomeList},
    methods: {
      tabClick(tab) {
        this.searchEchart(this.params)
      },
      searchEchart(params) {
        switch (this.tabNow) {
          case "total":
            this.$refs.echart1.query(params)
            this.$refs.echart2.query(params)
            break
          case "vs":
            this.$refs.echart3.query(params)
            break
        }
      },
      search(params) {
        this.$refs.list.query(params)
        this.searchEchart(params)
        this.params = params
      },
    }
  }
</script>

<style scoped>
  .box {
    margin: 0;
    background-color: #f0f0f0;
    padding-bottom: 20px;
  }

  .box .content {
    margin: 12px;
    background-color: white;
    padding: 18px;
  }
</style>
