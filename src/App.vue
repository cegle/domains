<template>
  <div id="app">
    <div class="header">
      <div class="title">{{title}}</div>
      <div class="contact">
        <div class="email el-tag">
          Mail-to:
          <a href="mailto:vip.qq.com">{{email}}</a>
        </div>
        <div class="qq el-tag">QQ: {{qq}}</div>
        <div class="googleVoice el-tag">GoogleVoice: {{googleVoice}}</div>
      </div>
    </div>
    <div class="main">
      <el-table
        v-loading="loading"
        :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
        stripe
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
    <div class="footer">
      <div class="copyright">{{copyright}}</div>
      <div class="site">
        <a :href="site">{{title}}</a>
      </div>
    </div>
    <scroll-top></scroll-top>
  </div>
</template>

<script>
import scrollTop from "./components/ScrollTop";

export default {
  name: "App",
  components: {
    "scroll-top": scrollTop
  },
  data() {
    return {
      title: "",
      email: "",
      qq: "",
      googleVoice: "",
      copyright: "",
      site: "",
      tableData: [],
      loading: true,
      search: ""
    };
  },
  methods: {},
  mounted() {
    this.$http
      .get("../static/data/domainsData.json")
      .then(res => {
        // console.log(res);
        if (res.status === 200) {
          this.loading = false;
          this.tableData = res.data.list;
          this.title = res.data.title;
          this.email = res.data.email;
          this.qq = res.data.qq;
          this.googleVoice = res.data.googleVoice;
          this.copyright = res.data.copyright;
          this.site = res.data.site;
        }
      })
      .catch(err => {
        console.log(err);
      });
  }
};
</script>

<style lang="scss" scoped>
#app {
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
    "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
  a {
    color: inherit;
    text-decoration: none;
  }
  max-width: 860px;
  margin: 0 auto;
  .header {
    border-bottom: 1px solid #eee;
    height: 90px;
    .title {
      font-size: 32px;
      line-height: 90px;
    }
    .contact {
      float: right;
    }
  }
  .main {
    margin-top: 50px;
  }
  .footer {
    height: 90px;
    text-align: center;
    font-size: 14px;
    padding-top: 35px;
    .site {
      margin-top: 10px;
      color: #409eff;
    }
  }
}
</style>
