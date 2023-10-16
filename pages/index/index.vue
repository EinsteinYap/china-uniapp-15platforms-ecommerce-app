<template>
<view>
	<!-- 顶部选项 -->
	<scroll-view 
	scroll-x 
	class="border-bottom scroll-row" 
	style="height: 80rpx;"
	:scroll-into-view="scrollinto"
	:scroll-with-animation="true">
		<view class="scroll-row-item px-3" 
		style="height: 80rpx;line-height: 80rpx;" 
		v-for="(item,index) in tabBars" :key="index"
	   :class="tabIndex===index? 'main-text-color border-bottom':''"
	   @click="changeTab(index)"
	   :id="'tab'+index"
			  >
		<!-- 记得新的滑动列表简短，但要绑定两个ID, :key 与 ：id -->
				<text class="font-md">{{item.name}}</text>
		</view>
		
	</scroll-view>
	<swiper :duration="150" 
	:current="tabIndex" 
	:style="'height:'+scrollH+'px;'"
	 @change="onChangeTab"
	 >
		<swiper-item v-for="(item,index) in newsitems" :key="index">
			<scroll-view scroll-y="true" :style="'height:'+scrollH+'px;'" @scrolltolower="loadmore(index)">  <!-- if not height, unable to scroll -->
			<block v-for="(list,listIndex) in item.list" :key="listIndex">
			<!-- 轮播图组件 -->
			<swiper-image v-if="list.type ==='swiper'" :resdata="list.data" />
			<template v-if="list.type ==='indexNavs'">
				<!-- 首页分类 -->
				<index-nav  :resdata="list.data" />
					<divider />
			</template>
			
			<template v-if="list.type ==='threeAdv'" >
				<!-- 	三图广告 -->
				<three-adv :resdata="list.data" />
				<divider />
			</template>	
			
			
			<!--大图广告位 -->	
			<!-- <card :showhead="true" headTitle="每日精选" bodyCover="../../static/images/demo/cate_banner.png" /> -->
			
			<!-- 公共列表组件 750 -5=745 = 372.5 -->
			<view class="row j-sb" v-else-if="list.type ==='list'">
				<block v-for="(item2,index2) in list.data" :key="index2">
				<common-list :item="item2" :index="index2"></common-list>
					
				</block>
				
			</view>
			</block>
			
			<!-- 上拉加载更多 -->
			<divider />
			<view class ="d-flex a-center j-center text-light-muted font-md py-3">
				{{item.loadtext}}
			</view>
			</scroll-view>
		</swiper-item>
	</swiper>
	

</view>

</template>

<script>
	
	let demoTabBars = [
		{
			name:"推存"
		},
		{
			name:"关注"
		},
		{
			name:"体育"
		},
		{
			name:"热点"
		},
		{
			name:"财经",
		},
		{
			name:"娱乐"
		},
		{
			name:"军事",
		},
		{
			name:"历史"
		},
		{
			name:"本地"
		}
	];
	
	let demo1 = [
		{
			type:"swiper",
			data:[
				{
					src:"../../static/images/demo/cate_banner.png"
				},
				{
					src:"../../static/images/demo/search-banner.png"
				},
				{
					src:"../../static/images/demo/cate_banner.png"
				}
			]
		},
		{
			type:"indexNavs",
			data:[
				{
					src:"../../static/images/indexnav/1.png",
					text:"新品发布"
				},
				{
					src:"../../static/images/indexnav/2.gif",
					text:"小米众筹"
				},
				{
					src:"../../static/images/indexnav/3.gif",
					text:"以旧换新"
				},
				{
					src:"../../static/images/indexnav/4.gif",
					text:"一份换团"
				},
				{
					src:"../../static/images/indexnav/5.gif",
					text:"超值特卖"
				},
				{
					src:"../../static/images/indexnav/6.gif",
					text:"小米秒杀"
				},
				{
					src:"../../static/images/indexnav/7.gif",
					text:"真心想要"
				},
				{
					src:"../../static/images/indexnav/8.gif",
					text:"电视热卖"
				},
				{
					src:"../../static/images/indexnav/9.gif",
					text:"家电热卖"
				},
				{
					src:"../../static/images/indexnav/10.gif",
					text:"米粉卡"
				}
			]
		},
		{
			type:"threeAdv",
			data:{
				big:{
					src:"/static/images/demo/demo1.jpg"
				},
				smalltop:{
					src:"/static/images/demo/demo2.jpg"
				},
				smallbotom:{
					src:"/static/images/demo/demo3.jpg"
				}
			}
		},
		{
			type:"list",
			data:[
			{
				cover:"/static/images/demo/list/1.jpg",
				title:"米家空调",
				desc:"1.5匹变率",
				oprice:2699,
				pprice:3999
				
			},
			{
				cover:"/static/images/demo/list/2.jpg",
				title:"黄家空调",
				desc:"1.5匹变率",
				oprice:6699,
				pprice:4399
				
			},
			{
				cover:"/static/images/demo/list/3.jpg",
				title:"李家空调",
				desc:"1.5匹变率",
				oprice:7699,
				pprice:5399
				
			},
			{
				cover:"/static/images/demo/list/4.jpg",
				title:"叶家空调",
				desc:"1.5匹变率",
				oprice:8699,
				pprice:7399
				
			}
			]
		}
	];
	
	let demo2 =[
		{
			type:"swiper",
			data:[
				{
					src:"../../static/images/demo/cate_banner.png"
				},
				{
					src:"../../static/images/demo/search-banner.png"
				},
				{
					src:"../../static/images/demo/cate_banner.png"
				}
			]
		},
		{
			type:"indexNavs",
			data:[
				{
					src:"../../static/images/indexnav/1.png",
					text:"新品发布"
				},
				{
					src:"../../static/images/indexnav/2.gif",
					text:"小米众筹"
				},
				{
					src:"../../static/images/indexnav/3.gif",
					text:"以旧换新"
				},
				{
					src:"../../static/images/indexnav/4.gif",
					text:"一份换团"
				},
				{
					src:"../../static/images/indexnav/5.gif",
					text:"超值特卖"
				},
									
			]
		},
		{
			type:"list",
			data:[
			
			{
				cover:"/static/images/demo/list/3.jpg",
				title:"李家空调",
				desc:"1.5匹变率",
				oprice:7699,
				pprice:5399
				
			},
			{
				cover:"/static/images/demo/list/4.jpg",
				title:"叶家空调",
				desc:"1.5匹变率",
				oprice:8699,
				pprice:7399
				
			}
			]
		}
	]
	
	import swiperImage from "@/components/index/swiper-image.vue";
	import indexNav from "@/components/index/index-nav";
	import threeAdv from "@/components/index/three-adv";
	import card from "@/components/common/card";
	import commonList from "@/components/common/common-list";
 	export default {
		components:{
			swiperImage,
			indexNav,
			threeAdv,
			card,
			commonList
		},
		data() {
			return {
				scrollinto:"",
				scrollH:500,
				tabIndex:0,
				tabBars:[],
				newsitems:[]
			}
		},
		onLoad() {
		//获取可视高度
		uni.getSystemInfo({
			success:(res)=>{
			this.scrollH = res.windowHeight - uni.upx2px(82)
			}
		})
		// 初始化事件
		this.__init()
		},
		methods: {
		// 初始化事件
		__init(){
			this.tabBars = demoTabBars
			
			let arr =[]
			for(var i=0 ; i<this.tabBars.length;i++){
				let obj = {
					list:[],
					loadtext:"上拉加载更多"
				}
				
				//获取首屏数据
				if(i===0){
					obj.list = demo1
				}
				arr.push(obj)
			}
			this.newsitems = arr
		},
		changeTab(index){
			//切换选项
			if(this.tabIndex ===index){
				return;
			}
			this.tabIndex= index	
			this.scrollinto ='tab' +index
			this.addData()
		},
		onChangeTab(e){
			//监听滑动列表
			this.tabIndex = e.detail.current
		},
		//加载数据
		addData(){
			let index = this.tabIndex
			this.newsitems[index].list = demo2
		},
		loadmore(index){
			//是否处于可加载状态
			let item = this.newsitems[index]
			if(item.loadtext !== '上拉加载更多')
				return;
				//模拟加载
				item.loadtext = '加载中...'
				setTimeout(()=>{
					//加载数据
					item.list = [...item.list,...demo2];
					//回复状态
					item.loadtext ='上拉加载更多'
				},2000)
		}
			
		
	}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
