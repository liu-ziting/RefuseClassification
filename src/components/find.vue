<template>
	<div class="find">
		<van-swipe class="topimgList" :autoplay="3000" :show-indicators="false" indicator-color="white">
		  <van-swipe-item>
			<img src="../assets/pic1.png" />
			<div class="van-ellipsis">这是一段最多显示一行的文字，多余的内容会被省略</div>
		  </van-swipe-item>
		  <van-swipe-item>
		  	<img src="../assets/pic1.png" />
			<div class="van-ellipsis">这是一段最多显示一行的文字，多余的内容会被省略</div>
		  </van-swipe-item>
		  <van-swipe-item>
		  	<img src="../assets/pic1.png" />
			<div class="van-ellipsis">这是一段最多显示一行的文字，多余的内容会被省略</div>
		  </van-swipe-item>
		</van-swipe>
		<h1>最新文章</h1>
		
		<newlist></newlist>
		
	</div>
</template>

<script>
	import newlist from './newList' //新闻列表
	
	export default {
		components: {
		    newlist
		}
	}
</script>

<style>
	.find{
		padding:0 0.625rem;
		box-sizing: border-box;
		padding-top: 0.8rem;
	}
	.find h1{
		font-size: 1.375rem;
	}
	.topimgList {
		border-radius: 0.3125rem;
	}
	.topimgList img{
		width: 100%;
		height: 12.5rem;
		object-fit:cover;
		display: block;
		border-radius: 0.3125rem;
	}
	.van-ellipsis{
		width: 100%;
		position: absolute;
		bottom: 0;
		color: #FFFFFF;
		font-size: 0.875rem;
		line-height: 2.2rem;
		padding-left: 0.625rem;
		background-color: rgba(0,0,0,0.5);
	}
</style>
