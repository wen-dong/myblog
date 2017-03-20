<template>
	<div class="app">
	<!-- 整个系统的头部 -->
	<mt-header fixed title="wend小超市" icon="more"></mt-header>
	 	<!--返回按钮-->
		<div class="back" v-if="isShow">
			<a @click="goback">返回</a>
		</div>

	<router-view></router-view>

	<!-- 整个系统的底部 -->
	<nav  class="mui-bar mui-bar-tab">
		<router-link class="mui-tab-item" to="/Home">
			<span class="mui-icon mui-icon-home"></span>
				<span class="mui-tab-label">首页</span>
		</router-link>

		<router-link class="mui-tab-item" to="/member">
		<span class="mui-icon mui-icon-contact">
				
			</span>
			<span class="mui-tab-label">会员</span>
		</router-link>

		<router-link class="mui-tab-item" to="/shopcar">
		<span class="mui-icon mui-icon-home">
			<span id="badge" class="mui-badge">0</span>
		</span>
			<span class="mui-tab-label">购物车</span>
		</router-link>

		<router-link class="mui-tab-item" to="/search">
			<span class="mui-icon mui-icon-gear"></span>
				<span class="mui-tab-label">搜索</span>
		</router-link>
	</nav>
	</div>
</template>

<script>
	import {vueobj} from './kits/commonvue.js';
	vueobj.$on('shopdata',function(data){
		let badge = document.getElementById('badge');
		let count = badge.innerText - 0; // 获取原始值
		count+=data;  // 在原始值上增加新数据

		// 将新数据同步到dom中
		badge.innerText = count;
	});

	export default{
		data(){
			return {
				isShow:false 
			}
		},
		watch:{
			'$route':function(newval,oldval){
				if(newval.path.toLowerCase() == '/home'){
					//表示当前页面是首页应该要隐藏返回按钮
					this.isShow = false;
				}else{
					//非首页要显示返回按钮
					this.isShow = true;
				}
			}
		},
		methods:{
			goback(){
				this.$router.go(-1); //返回上一个页面
			}
		}
	}

</script>

<style scoped>
	.back{
		position: fixed;
		top:10px;
		left:10px;
		z-index: 50;
	}
	.back a{
		font-size: 16px;
		color: #fff;
		font-weight:bold;
	}
</style>