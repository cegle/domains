<template>
  <div id="app">
    <div class="header">
      <div class="logo"></div>
    </div>
    <div class="main">
      <el-table
        v-loading="loading"
        :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
        style="width: 100%"
      >
        <el-table-column label="域名列表" prop="name"></el-table-column>
        <el-table-column label="价格">
          <template slot-scope="scope">
            <el-tag>{{scope.row.price}}</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="备注" align="center">
          <template slot="header" slot-scope="scope">
            <el-input v-model="search" size="mini" placeholder="输入域名关键字搜索"/>
          </template>
          <template slot-scope="scope">{{scope.row.desc}}</template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      tableData: [
        {
          name: "acg.tc",
          price: "100",
          desc: "acg"
        },
        {
          name: "vpsbird.com",
          price: "5000",
          desc: "搞VPS的"
        },
        {
          name: "2016-05-01",
          price: "王小虎",
          desc: "上海市普陀区金沙江路 1519 弄"
        },
        {
          name: "2016-05-03",
          price: "王小虎",
          desc: "上海市普陀区金沙江路 1516 弄"
        }
      ],
      loading: false,
      search: ""
    };
  },
  methods: {}
};
</script>

<style lang="scss" scoped>
#app {
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
    "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
  .header {
    height: 120px;
    border: 1px solid red;
  }
  .main {
    max-width: 860px;
    margin: 0 auto;
  }
}
</style>
