<template>
	
	<view class="d-flex">
		<image :src="resdata.big.src" lazy-load style="width: 373upx;height: 530upx;border-right: 2upx solid #F5F5F5;" mode="aspectFill" class="img img-fluid" @tap="event(resdata.big)" />
		
		<view class="d-flex flex-column">
			<image :src="resdata.smalltop.src" style="width: 375upx;height: 264upx;border-bottom:2upx solid #F5F5F5;" class="img img-fluid" @tap="event(resdata.smalltop)" />
			<image :src="resdata.smallbotom.src" style="width: 375upx;height: 264upx;" mode="aspectFill" class="img img-fluid" @tap="event(resdata.smallbotom)" />
			
		</view>
		
	</view>
</template>

<script>
	export default {
		props:{
			resdata:Object
		},
		methods:{
			event(obj){
				console.log(obj)
			}
		}
	}
	
</script>

<style>
</style>