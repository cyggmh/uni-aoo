<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
		<view class="text-area">
			<!-- <text class="title">{{title}}</text> -->
			<view v-for="arr in list" :key="arr.id" style="display: block;"><view>{{arr.name}}</view></view>
		</view>
	</view>
</template>

<script>
	var app = getApp().globalData;
	export default {
		data() {
			return {
				title: 'Hello',
				list:[]
			}
		},
		onLoad() {
			uni.request({
				url: app.url+'home',
				method: 'GET',
				withCredentials: true, // 携带跨域cookie
				header: {
					'content-type': 'application/x-www-form-urlencoded'
				},
				data: {
					id:1
				},
				success: res => {
					console.log(res)
					if(res.data.code == 200){
						this.list = res.data.data
					}else{
							uni.showModal({
								content: 'bbb',
								showCancel: false
							});
					}
				},
				fail: () => {
					uni.showModal({
						content: 'aaaa',
						showCancel: false
					});
				},
				complete: () => {}
			});
			uni.request({
				url: app.url+'userInfo',
				method: 'POST',
				withCredentials: true, // 携带跨域cookie
				header: {
					'content-type': 'application/x-www-form-urlencoded'
				},
				data: {
					id:1
				},
				success: res => {
					console.log(res)
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {

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
