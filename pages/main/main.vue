<template>
	
<view class = "container">
	<!--pages/main/main_page.wxml-->
	<!--0：管理员，1：车间管理人员，2：QC,3:焊工-->
	<view class="title-box">
	    <view class = "main_text-logo">
	    <image class ="icon-picture-logo" src="../image/CFHI_logo.png"></image>
	    </view>
	    <view v-show="classCode === 2">
			<view class = "textMain">请选择当前检验内容</view>
		</view>
		<view v-show="classCode === 3">
		    <view class = "textMain">请选择当前报检内容</view>
		</view>
		<view v-show="classCode === 0">
		    <view class = "textMain">请选择所需功能</view>
		</view>
	</view>
	
	<view class="blanke-box"></view>
	<!--间隔灰横条-->
	<view class="graydivide"></view>
	<view class='func-box'>
	<view v-if=" classCode === 2 || classCode === 0">
	
		<view class="func-column" @click="jump2inspectFitUp"><!--左边图片&文字-->
	    <image class="icon-picture" src="../image/logo.png"></image>
	    
	    <view class="text">组对检验信息提交</view><!--文字-->
	    </view>
		<view class="graydivide"></view>
		<view class="func-column" @click="jump2inspectVisual"><!--左边图片&文字-->
		<image class="icon-picture" src="../image/logo.png"></image>
		
		<view class="text">外观检验信息提交</view><!--文字-->
		</view>
		
	</view>
	<view class="graydivide"></view>

	<view v-if="classCode === 3 || classCode === 0">
		<view class="func-column" @click="jump2fitup"><!--左边图片&文字-->
		<image class="icon-picture" src="../image/logo.png"></image>
		
		<view class="text">组对信息提交</view><!--文字-->
		</view>
		<view class="graydivide"></view>
		<view class="func-column" @click="jump2weld"><!--左边图片&文字-->
		<image class="icon-picture" src="../image/logo.png"></image>
		
		<view class="text">焊接信息提交</view><!--文字-->
		</view>
	    <view class="graydivide"></view>	
	</view>	
		
    </view>
	
</view>


</template>

<script>
	export default {
		data() {
			return {
				classCode : 0,
			}
		},
		onLoad(){
			this.classCode = getApp().globalData.classCode
			
			
		},
		methods: {
			jump2inspectFitUp(){
				getApp().globalData.activityType = 'inspectFitUp'
				uni.navigateTo({
					
					url:'/pages/inspectFitUp/inspectFitUp'
				})
				
			},
			jump2inspectVisual(){
				getApp().globalData.activityType = 'inspctVisual'
				uni.navigateTo({
					url:'/pages/shaoma/shaoma'
				})
				
			},
			jump2fitup(){
				getApp().globalData.activityType = 'fitUp'
				uni.navigateTo({
					url:'/pages/shaoma/shaoma'
				})
				
			},
			jump2weld(){
				getApp().globalData.activityType = 'weld'
				uni.navigateTo({
					url:'/pages/shaoma/shaoma'
				})
				
			}
			
		}
	}
</script>

<style>
/* pages/main/main_page.wxss */
.title-box{
	width: 100%;
	height: 40%;
	display: flex;
	flex-direction: row;
	align-items: center;
	
}
.blanke-box{
	height: 60px;
	
	
}
.icon-picture-logo{
	width: 50px;
	height: 50px;
}
.textMain{
	margin-left: 6px;
	font-size: 24px;
	
}
.text{
	margin-left: 6px;
	font-size: 18px;
	
	
}
/* 功能键容器 */
.func-box{
	width: 100%;
	height: 60%;
	display: flex;
	flex-direction: column;
}
.func-column{
	width: 100%;
	height: 40px;
	display: flex;
	flex-direction: row;
	align-items: center;
	margin-top: 4px;
	margin-bottom: 4px;
}
.icon-picture{
	width: 20px;
	height: 20px;	
}

</style>
