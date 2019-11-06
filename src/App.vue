<template>
  <div id="app">
	<!-- 标题 -->
	<!-- <van-nav-bar class="toptitle" v-bind:title="title">
	</van-nav-bar> -->
	<!-- 中间模块 -->
	<component class="main" :is="cmpName"></component>
	<!-- 底部导航栏 -->
	<van-tabbar v-model="active">
	  <!-- <van-tabbar-item v-on:click="changeCmp('mainTab',$event)"  icon="wap-home-o">主页</van-tabbar-item>
	  <van-tabbar-item v-on:click="changeCmp('findTab',$event)"  icon="apps-o">发现</van-tabbar-item>
	  <van-tabbar-item v-on:click="changeCmp('wode',$event)" icon="friends-o">我的</van-tabbar-item> -->
	</van-tabbar>
	
  </div>
</template>

<script>
import mainTab from './components/main.vue' //主页
// import findTab from './components/find.vue' //发现
// import wode from './components/wode.vue' //我的

export default {
	name: 'app',
	components: {
		mainTab,
		// findTab,
		// wode
	},
	data() {
		return {
			active: 0,
			cmpName:'mainTab',//默认显示第一个组件
			title:'主页'
		}
	},
	methods : {
		changeCmp(cmpName,$event) {
			// 动态改变标题
			// this.title = $event.target.innerText;
			// 切换模块
		    this.cmpName = cmpName;
		}
	},
}
</script>

<style>
	body{
		background-color: #FFFFFF;
	}
	.main{
		width: 100%;
		height: auto;
		padding-bottom: 3.125rem;
	}
	.toptitle{
		width: 100%;
		position: fixed !important;
		top: 0;
	}
</style>
