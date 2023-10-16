<template>
	<view class="">
		<swiper indicator-dots autoplay :interval="3000" :duration="1000" circular>
			<block v-for="(item,index) in resdata" :key="index">
			<swiper-item>
				<view class="swiper-item">
					<image :src="item.src" lazy-load style="height: 350upx;" @tap="event(item)" />
				</view>
			</swiper-item>
			</block>
		</swiper>
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Array
		},
		methods:{
			event(item){
				console.log('点击轮播图')
			}
		}
	}
</script>

<style>
</style>