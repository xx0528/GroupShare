
 <template>
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
	<view>
		<u-grid :border="false" col="5" @click="clickGridItem">
			<u-grid-item
					v-for="(listItem,listIndex) in centerBtnList"
					:key="listIndex"
			>
				<u-image width="50rpx" height="50rpx" :src="listItem.image"></u-image>
				<text class="grid-text">{{listItem.title}}</text>
			</u-grid-item>
		</u-grid>
	</view>
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
				
				<view class="group-btn"><u-button type="primary" size="mini" @click="handleUpdateUser()">{{item.btnStr}}</u-button></view>
			</view>
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
			image: '/static/image/btn_home1.png',
			title: '发布群'
			},
			{
				image: '/static/image/btn_home2.png',
				title: '悬赏群'
			},
			{
				image: '/static/image/btn_home4.png',
				title: '分享赚佣金'
			},
			{
				image: '/static/image/btn_home9.png',
				title: '广告群发'
			},
			{
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
			image : 'https://cdn.uviewui.com/uview/album/1.jpg',
			name: 'xx行业客户群1',
			member: '232人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/2.jpg',
			name: 'xx行业群',
			member: '22人群',
			location: '深圳市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/3.jpg',
			name: 'xx行业客户群2',
			member: '232人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/4.jpg',
			name: 'xx行业客户群3',
			member: '342人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '共享',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/5.jpg',
			name: '客户群8',
			member: '232人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/6.jpg',
			name: 'xx行业客户群1',
			member: '2772人群',
			location: '北京市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/7.jpg',
			name: 'xx行业客2户群2',
			member: '92人群',
			location: 'xx市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/8.jpg',
			name: 'xx行43业客户群1',
			member: '202人群',
			location: '长沙市',
			source: '管理员共享',
			btnStr: '加群',
		},
		{
			image : 'https://cdn.uviewui.com/uview/album/9.jpg',
			name: 'xx行业客户群1',
			member: '756人群',
			location: '广州市',
			source: '管理员共享',
			btnStr: '加群',
		},
	])
	const clickGridItem = (name: string) => {
		console.log("点击了--" + name)
	}
	
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
	
</script>

<style lang="scss" scoped>
	.top {
		padding: 8rpx 8rpx;
		.u-search {
			padding: 25rpx 25rpx 0rpx;
		}
	}
	.group-content {
		display: flex;
		.group-item {
			display: flex;
			width: 100%;
			justify-content: start;
			align-items: center;
			border-top: 3rpx solid $uni-main-color;
			.u-image{
				margin: 20rpx;
			}
			.group-text {
				display: flex;
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
