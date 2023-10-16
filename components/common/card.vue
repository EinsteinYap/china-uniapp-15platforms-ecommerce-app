<template>
<view class="card">
		<view v-if="showhead" class="p-2 border-bottom main-border-color">
			<slot name="title">
		<text v-if="headTitle" class="font-md font-weight ">{{headTitle}}</text>		
			</slot>
		</view>
		<image v-if="bodyCover" :src="bodyCover" mode="widthFix" />
		<slot name="body"></slot>
	</view>
</template>

<script>
export default {
	props:{
		headTitle:String,
		bodyCover:String,
		showhead:{
		type:Boolean,
		default:false
		}
	}
}
</script>

<style>
</style>