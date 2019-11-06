<template>
	<div class="mainBox">
		<van-row>
			<van-col span="24">
				<img src="../assets/topban.png" />
			</van-col>
		</van-row>
		<van-row class="imgList">
			<van-col v-on:click="showPopup('khs')"title='可回收垃圾'  span="6">
				<img src="../assets/khs1.png" />
			</van-col>
			<van-col v-on:click="showPopup('yhlj')" span="6" title='有害垃圾' >
				<img src="../assets/yhlj1.png" />
			</van-col>
			<van-col v-on:click="showPopup('slj')" span="6" title='湿垃圾' >
				<img src="../assets/slj1.png" />
			</van-col>
			<van-col v-on:click="showPopup('glj')"  span="6" title='干垃圾' >
				<img src="../assets/gl1j.png" />
			</van-col>
		</van-row>
		<van-search @clear="onClear" @input="oninput"  @search="onSearch"  v-model="value"  class="search" placeholder="请输入搜索关键词" />
		<div class="van-ellipsis">提示：请输入关键词进行搜索...</div>
		<h1 v-if="garbageShow" v-bind:style="styleObject">{{garbage}}</h1>
		<!-- 弹出层 -->
		<van-popup
		  v-model="show"
		  closeable
		  position="bottom"
		>
		<div v-if="khs">
			<h2>可回收垃圾</h2>
			<p>就是可以再生循环的垃圾，本身或材质可再利用的纸类、硬纸板、玻璃、塑料、金属、塑料包装等</p>
			<h2>投放要求</h2>
			<ul>
				<li>1、轻投轻放</li>
				<li>2、清洁干燥，避免污染</li>
				<li>3、废纸尽量平整</li>
				<li>4、立体包装请清空内容物，清洁后压扁投放</li>
				<li>5、有尖锐边角的，应包裹后投放</li>
			</ul>
		</div>
		<div v-if="yhlj">
			<h2>有害垃圾</h2>
			<p>指废电池、废灯管、废药品、废油漆及其容器等对人体健康或者自然环境造成直接或者潜在危害的生活废弃物。常见包括废电池、废荧光灯管、废灯泡、废水银温度计、废油漆桶、过期药品、过期化妆品等。有害有毒垃圾需特殊正确的方法安全处理。</p>
			<h2>投放要求</h2>
			<ul>
				<li>1、轻投轻放</li>
				<li>2、易破损的请连带包装或包裹后轻放</li>
				<li>3、如易挥发，请密封投放</li>
			</ul>
		</div>
		<div v-if="slj">
			<h2>湿垃圾</h2>
			<p>是指居民日常生活及食品加工、饮食服务、单位供餐等活动中产生的垃圾，包括丢弃不用的菜叶、剩菜、剩饭、果皮、蛋壳、茶渣、骨头等，其主要来源为家庭厨房、餐厅、饭店、食堂、市场及其他与食品加工有关的行业。</p>
			<h2>投放要求</h2>
			<ul>
				<li>1、纯流质的食物垃圾，如牛奶等，应直接倒入下水道</li>
				<li>2、有包装物的湿垃圾应该将包装物去除后分类投放，包装物请投放对应的可回收物或者干垃圾容器</li>
			</ul>
		</div>
		<div v-if="glj">
			<h2>干垃圾</h2>
			<p>是危害较小，但无再次利用价值，如建筑垃圾类，生活垃圾类等，一般采取填埋、焚烧、卫生分解等方法，部分还可以使用生物解决，如放蚯蚓等。是可回收垃圾、厨余垃圾、有害垃圾剩余下来的一种垃圾。</p>
			<h2>投放要求</h2>
			<ul>
				<li>1、尽量沥干水分</li>
				<li>2、难以辨识类别的生活垃圾投入干垃圾容器内</li>
			</ul>
		</div>
		</van-popup>
	</div>
	
</template>

<script>
	import axios from 'axios'
	import { Dialog } from 'vant';
	
	
	export default {
	  data() {
	    return {
	      show: false,
		  khs:false,
		  yhlj:false,
		  slj:false,
		  glj:false,
		  value:'',
		  garbage:'',
		  garbageShow:false,
		  styleObject:{
			color: 'red'
		  },
	    }
	  },
	  methods: {
	    showPopup(cmpName) {
		  //弹出层
	      this.show = true;
		  this.khs = false;
		  this.yhlj = false;
		  this.slj = false;
		  this.glj = false;
		  this[cmpName] = true;
		  
	    },
		onSearch(value){
			//点击搜索的时候
			var toast = this.$toast.loading({message: '查询中...'});
			var UrlPath = "https://www.mxnzp.com/api/"
			axios
			  .get(UrlPath+'rubbish/type?name='+value+'')
			  .then(response => {
				  var result = response.data;
				  this.garbageShow = true;
				  toast.clear();
				  if(result.code == "1"){
					  this.garbage = '（'+result.data.aim.goodsType+'）';
				  }else{
					  Dialog({ message: result.msg });
				  }
			})
			.catch(function (error) { // 请求失败处理
				console.log(error);
			});
		},
		onClear(){
			//点击搜索框的清除的回调
			 this.garbage = '';
		},
		oninput(){
			//删除搜索框里面的文字的回调
			 this.garbage = '';
		}
	  }
	};
</script>

<style>
	.mainBox img{
		width: 100%;
	}
	.mainBox .imgList{
		width: 90%;
		margin-left: 5%;
		margin-top: 1.25rem;
	}
	.mainBox .imgList img{
		width: 92%;
		display: block;
		margin: 0 auto;
		height: 5.2rem;
	}
	.mainBox .search{
		margin-top: 1.5625rem;
		width: 90%;
		margin-left: 5%;
	}
	.mainBox .search input{
		height: 2.5rem;
		font-size: 1.0625rem;
	}
	.mainBox .search .van-field__left-icon{
		line-height: 2.5rem;
	}
	.mainBox .van-ellipsis{
		width: 90%;
		margin-left: 5%;
		padding: 0 0.75rem;
		box-sizing: border-box;
		font-size: 0.875rem;
		color: #666666;
	}
	.mainBox h2,p,ul{
		padding: 0 0.625rem !important;
		color: #666666;
	}
	.mainBox h2{
		font-size: 1.125rem;
		margin-bottom: 0.625rem;
		color: #393D49;
	}
	.mainBox ul{
		margin-bottom: 1.25rem !important;
	}
	.mainBox h1{
		width: 100%;
		text-align: center;
		margin-top: 6.25rem;
	}
</style>
