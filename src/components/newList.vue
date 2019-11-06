<template>
	<div class="newList">
		 <ul>
			 <li v-for="item in items" :key="item.id">
				<img v-bind:src="item.imgList" />
				<div class="van-multi-ellipsis--l2">{{ item.title }}</div>
				<p>{{ item.source }}</p>
				<time>
					{{ item.postTime }}
				</time>
			 </li>
		 </ul>
	</div>
</template>

<script>
	import axios from 'axios'
	import { Dialog } from 'vant';
	
	export default {
		data() {
		  return {
			  loading: false,
			  finished: false,
			  items: [{
				  title: '这是一个标题这是一个标题这是一个标题',
				  source: '数字尾巴',
				  postTime: '10-25',
				  imgList: 'img/pic1.41b2ab0d.png',
				  id: ""
			  }]
		  }
		},
		mounted(){
			
		},
		methods: {
			
		}
	}
</script>

<style>
	ul{
		padding: 0 !important;
	}
	.newList img{
		width: 6.50rem;
		height: 5rem;
		display: block;
		float: left;
		margin-right: 0.625rem;
		border-radius: 0.1rem;
	}
	.newList .van-multi-ellipsis--l2{
		height: 4rem;
		color: #000;
		margin: 0;
		padding: 0;
		line-height: 1.25rem;
	}
	.newList li{
		position: relative;
		overflow: hidden;
		margin-bottom: 0.9375rem;
	}
	.newList p{
		font-size: 0.75rem;
		color: #666666;
		margin: 0;
		float: left;
		padding: 0 !important;
	}
	.newList time{
		float: right;
		font-size: 0.75rem;
		color: #666666;
		position: absolute;
		bottom: 0;
		right: 0;
	}
	.newList time .van-icon{
		display: block;
		float: left;
		margin-right: 0.1875rem;
	}
</style>
