
 <template>
	<view>
		<view class="top">
			<u-swiper
					:list="swiperList"
					keyName="image"
					showTitle
					:autoplay="true"
					circular
			></u-swiper>
			
			<u-search placeholder="输入关键字搜索群" v-model="searchStr" inputAlign="center" @click="goSearchPage()" :showAction="false"></u-search>
		</view>
		<u-sticky>
			<view class="center">
				<u-grid :border="false" col="5">
					<u-grid-item
							v-for="(listItem,listIndex) in centerBtnList"
							:key="listIndex"
							@click="goEnterPage(listItem.id)"
					>
						<u-image width="50rpx" height="50rpx" :src="listItem.image"></u-image>
						<text class="grid-text">{{listItem.title}}</text>
					</u-grid-item>
				</u-grid>
			</view>
		</u-sticky>
		<view>
			<view class="group-content" v-for="(item, itemIdx) in groupList">
				<view class="group-item">
					<u-image width="100rpx" height="100rpx" :src="item.image"></u-image>
					<view class="group-text">
						<text>{{item.name}}</text>
						<view class="item-text">
							<text>{{item.member}}</text>
							<text>{{item.location}}</text>
							<text>{{item.source}}</text>
						</view>
					</view>
					
					<view class="group-btn"><u-button :type="item.shareType === 1 ? 'primary' : 'success'" size="middle" @click="goGroupPage(item.shareType)">{{item.btnStr}}</u-button></view>
				</view>
			</view>
		</view>
		<view>
			<u-modal :show="dialogInfo.show" :showCancelButton="true"
			 title="付费进群" :content="dialogInfo.content" :zoom="false"
			 @confirm="joinGroup" @cancel="closeDialog"></u-modal>
			<!-- <u-modal :show="dialogInfo.show" title="付费进群" :content='dialogInfo.content' :zoom="true"></u-modal> -->
		</view>
		
	</view>
</template>

<script setup lang="ts">
	import { reactive, ref } from "vue";
	import { onLoad, onShow } from '@dcloudio/uni-app'
	
	const searchStr = ref("")
	const swiperList = reactive([{
			image: 'https://cdn.uviewui.com/uview/swiper/swiper2.png',
			title: '昨夜星辰昨夜风，画楼西畔桂堂东'
		},{
			image: 'https://cdn.uviewui.com/uview/swiper/swiper1.png',
			title: '身无彩凤双飞翼，心有灵犀一点通'
		},{
			image: 'https://cdn.uviewui.com/uview/swiper/swiper3.png',
			title: '谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳'
		}])
	const centerBtnList = reactive([
		{
			id: 1,
			image: '/static/image/btn_home1.png',
			title: '发布群'
		},
		{
			id: 2,
			image: '/static/image/btn_home2.png',
			title: '悬赏群'
		},
		{
			id: 3,
			image: '/static/image/btn_home4.png',
			title: '分享赚佣金'
		},
		{
			id: 4,
			image: '/static/image/btn_home9.png',
			title: '广告群发'
		},
		{
			id: 5,
			image: '/static/image/btn_home10.png',
			title: '物品交易'
		},
		])
	const indexList = reactive([])
	const urls = reactive([
						'https://cdn.uviewui.com/uview/album/1.jpg',
						'https://cdn.uviewui.com/uview/album/2.jpg',
						'https://cdn.uviewui.com/uview/album/3.jpg',
						'https://cdn.uviewui.com/uview/album/4.jpg',
						'https://cdn.uviewui.com/uview/album/5.jpg',
						'https://cdn.uviewui.com/uview/album/6.jpg',
						'https://cdn.uviewui.com/uview/album/7.jpg',
						'https://cdn.uviewui.com/uview/album/8.jpg',
						'https://cdn.uviewui.com/uview/album/9.jpg',
						'https://cdn.uviewui.com/uview/album/10.jpg',
					])
	const groupList = reactive([
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/1.jpg',
			name: 'xx行业客户群1',
			member: '232人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 2,
			image : 'https://cdn.uviewui.com/uview/album/2.jpg',
			name: 'xx行业群',
			member: '22人群',
			location: '深圳市',
			source: '管理员共享',
			btnStr: '共享',
		},
		{
			shareType : 2,
			image : 'https://cdn.uviewui.com/uview/album/3.jpg',
			name: 'xx行业客户群2',
			member: '232人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '共享',
		},
		{
			shareType : 2,
			image : 'https://cdn.uviewui.com/uview/album/4.jpg',
			name: 'xx行业客户群3',
			member: '342人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '共享',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/5.jpg',
			name: '客户群8',
			member: '232人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/6.jpg',
			name: 'xx行业客户群1',
			member: '2772人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/7.jpg',
			name: 'xx行业客2户群2',
			member: '92人群',
			location: 'xx市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 2,
			image : 'https://cdn.uviewui.com/uview/album/8.jpg',
			name: 'xx行43业客户群1',
			member: '202人群',
			location: '长沙市',
			source: '管理员共享',
			btnStr: '共享',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			shareType : 1,
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
	])
	const dialogInfo = reactive({
		show : false,
		title: "",
		content: ""
	})
	onLoad(() => {
		loadmore()
	})
	onShow(() => {
	})
	
	const scrolltolower = () => {
		loadmore()
	}
	
	const loadmore = () => {
		for (let i = 0; i < 30; i++) {
			indexList.push({
				url: urls[uni.$u.random(0, urls.length - 1)]
			})
		}
	}
	
	const goSearchPage = () =>{
		uni.navigateTo({
			url:'/pages/search/search'
		})
	}
	
	const goGroupPage = (shareType : number) => {
		if (shareType === 1) {
			dialogInfo.show = true
			dialogInfo.content = "花费50积分获取群主微信"
		} else if (shareType === 2) {
			uni.navigateTo({
				url: '/pages/find-group/find-group'
			})
		}
	}
	
	const goEnterPage = (id: number) => {
		var url : string = ''
		switch(id) {
			case 1:
				url = '/pages/share-group/share-group'
				break
			case 2:
				url = '/pages/find-group/find-group'
				break
			case 3:
				url = '/pages/advertise/advertise'
				break
			case 4:
				url = '/pages/task/task'
				break
			case 5:
				url = '/pages/trade/trade'
				break
			default:
				url = '/pages/home/home'
		}
		uni.navigateTo({
			url
		})
	}
	
	const joinGroup = () => {
		dialogInfo.show = false
		
	}
	
	const closeDialog = () => {
		dialogInfo.show = false
	}
	
</script>

<style lang="scss" scoped>
	.top {
		padding: 0rpx 4rpx;
		.u-search {
			padding: 25rpx 25rpx 0rpx;
		}
	}
	.center {
		background-color: $uni-bg-color;
		.grid-text {
			font-size: 28rpx;
		}
		padding: 20rpx 0rpx 20rpx;
	}
	.group-content {
		display: flex;
		.group-item {
			display: flex;
			width: 100%;
			justify-content: flex-start;
			align-items: center;
			padding: 10rpx 20rpx 10rpx;
			border-top: 3rpx solid $uni-main-color;
			.u-image{
				margin: 20rpx;
			}
			.group-text {
				display: flex;
				margin-left: 20rpx;
				flex-direction: column;
				text{
					font-weight: bold;
				}
				.item-text {
					display: flex;
					font-size: 14rpx;
					margin-top: 10rpx;
					text{
						margin-right: 20rpx;
					}
				}
			}
			.group-btn {
				width: 150rpx;
				margin-left: auto;
			}
		}
	}
</style>
