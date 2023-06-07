<template>
	<view class="user">
		<view class="user-header" @click="handleUserOption('/pages/user/user-Info')">
			<!-- <u-avatar :src="userInfo.avatar?userInfo.avatar:'/static/image/default-avatar.png'" shape="circle" size="large"></u-avatar> -->
			<u-avatar :src="userInfo.avatar" shape="circle" size="large"></u-avatar>
			<view class="user-name">{{userInfo.username?userInfo.username:'登录后查看更多精彩'}}</view>
		</view>
		<view class="user-options">
			<u-cell-group v-for="(item, idx) in cellList" >
				<u-cell-item :title="item.name" :icon="item.img" size="large"
					@click="onClickCell(item.id)"></u-cell-item>
			</u-cell-group>
		</view>

	</view>
</template>

<script lang="ts" setup>
	import { onActivated, nextTick, onMounted, reactive, ref, toRefs, computed, watch, watchEffect } from 'vue'
	import { onLoad, onShow, onReady, onHide } from '@dcloudio/uni-app'
	import { useUser } from '@/stores/user'
	import {wxIsLogin} from '@/utils/wxLogin'
	const userStore = useUser()
	const state = reactive({
		userInfo: {
			avatar: '',
			username: '',
		}
	})
	
	const { userInfo } = toRefs(state)

	const cellList = reactive([
		{
			id : 1,
			name : "个人中心",
			img : "/static/image/btn_mine1.png",
		},
		{
			id : 2,
			name : "VIP等级",
			img : "/static/image/btn_mine2.png",
		},{
			id : 3,
			name : "佣金提现",
			img : "/static/image/btn_mine3.png",
		},{
			id : 4,
			name : "宇宙群主",
			img : "/static/image/btn_mine4.png",
		},{
			id : 5,
			name : "我的社群",
			img : "/static/image/btn_mine5.png",
		},{
			id : 6,
			name : "充值送金币",
			img : "/static/image/btn_mine6.png",
		},{
			id : 7,
			name : "我的订单/任务",
			img : "/static/image/btn_mine7.png",
		},{
			id : 8,
			name : "联系客服",
			img : "/static/image/btn_mine8.png",
		},{
			id : 9,
			name : "下载APP",
			img : "/static/image/btn_mine9.png",
		},
	])
	onLoad(() => {

		// #ifdef MP-WEIXIN
		if(wxIsLogin()) return
		// #endif
		userInfo.value.username = userStore.userInfo.username
		userInfo.value.avatar = userStore.userInfo.avatar

	})
	onShow(() => {
		// load()
	})
	onActivated(() => {
		// activated()
	})
	onMounted(() => {

	})



	watch(() => userStore.userInfo.username, () => {
		if (userStore.token) {
			userInfo.value.username = userStore.userInfo.username
		}
	})
	watch(() => userStore.userInfo.avatar, () => {
		if (userStore.token) {
			userInfo.value.avatar = userStore.userInfo.avatar
		}
	})

	const onClickCell = (id : number) => {
		
		switch(id) {
			case 1:
				handleUserOption('/pages/user/user-Info')
				break;
			case 2:
				break;
			case 3:
				break;
			case 4:
				break;
			case 5:
				break;
			default:
			}
			
			uni.showToast({
				title: '点击了cell' + id,
				icon: 'none',
				position: 'top'
			})
	}

	const handleUserOption = (url : string) => {
		uni.navigateTo({
			url
		})
	}
</script>

<style lang="scss" scoped>
	.user-header {
		width: 100%;
		height: 180rpx;
		background-color: $uni-main-color;
		border-radius: 0 0 40rpx 40rpx;
		display: flex;
		justify-content: center;
		align-items: center;

		.user-name {
			margin-left: 20rpx;
			color: #fff;
		}

	}

	.user-options {
		margin-top: 30rpx;


	}
</style>