<template>
	<div id="app">
		<div class="header">
			<div class="logo">Domains</div>
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
						this.tableData = res.data;
						this.loading = false;
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
	.header {
		height: 90px;
		// border: 1px solid red;
		text-align: center;
		.logo {
			font-size: 32px;
			line-height: 90px;
		}
	}
	.main {
		max-width: 860px;
		margin: 0 auto;
	}
}
</style>
