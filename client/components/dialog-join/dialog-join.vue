<!-- prompt组件 -->
<!-- prompt -->
<template>
	<view class="prompt-box" v-if="isHidden==true">
		<view class="prompt-content contentFontColor">
			<view class="prompt-title">
				<text class="title-text">{{title}}</text>
				<view class="img-tit" @click="_confirm"></view>
			</view>
			<rich-text class="prompt-text" :nodes="text"></rich-text>
			<view class="prompt-btn-group">
				<text class="title-text" @click="_confirm">{{btn_certain}}</text>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				multipleSlots: true,// 在组件定义时的选项中启用多slot支持
				isHidden: false,
				cost:''
			};
		},
		props:{
			title: {            
			  type: String,    
			  default: '关于我们'    
			},
			btn_certain: {
			  type: String,
			  default: '知道了'
			},
			text:{
				type: String,
				default: '未加载成功',
			},
			dialogVisible:{
				type:Boolean,
				default:false
			}
		},
		watch:{
			dialogVisible(val) {
			  if (val === false) {
			  } else {
				this.show()
			  }
			}
		},
		// created() {
		// 	this.isHidden = this.dialogVisible
		// },
		methods: {
			hide () {
			  this.isHidden=false;
			},
			show(e) {
			  this.isHidden=true;
				if(e!=null&&e!=undefined&&e!=""){
					this.text = e;
				}
			},
			/*
			 * 内部私有方法建议以下划线开头
	 		 * triggerEvent 用于触发事件
			 */
			_confirm () {
			  this.hide()
			  this.$emit('onConfirm', '');
			}
		}
	}
</script>
 
<style>
/* components/vas-prompt/vas-prompt.wxss */
.prompt-box {
  position: absolute;
  left: 0;
  top: 0;
  width: 750rpx;
  height: 100%;
  z-index: 11;
  background: rgba(0, 0, 0, 0.5);
}
 
.prompt-content {
  position: absolute;
  left: 50%;
  top: 40%;
  width: 700rpx;
  max-width: 700rpx;
  border-radius: 8rpx;
  transform: translate(-50%, -50%); 
  overflow: hidden;
  background: #fff;
}
 
.prompt-title {
  width: 100%;
  padding: 20rpx;
  text-align: center;
  height: 25rpx;
  line-height: 25rpx;
  background-color:#E73C2F;
}
.title-text{
	font-size: 32rpx;
	color: white;
}
.img-tit{
    position: absolute;
    right: 20rpx;
    top: 15rpx;
    width: 30rpx;
    height: 30rpx;
    background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABwAAAAcCAYAAAByDd+UAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyZpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMTQ1IDc5LjE2MzQ5OSwgMjAxOC8wOC8xMy0xNjo0MDoyMiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTkgKFdpbmRvd3MpIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOjg0RUNFQTFDNjcyNjExRTk4MkIwQzcyMzlDQ0UwOTM5IiB4bXBNTTpEb2N1bWVudElEPSJ4bXAuZGlkOjg0RUNFQTFENjcyNjExRTk4MkIwQzcyMzlDQ0UwOTM5Ij4gPHhtcE1NOkRlcml2ZWRGcm9tIHN0UmVmOmluc3RhbmNlSUQ9InhtcC5paWQ6ODRFQ0VBMUE2NzI2MTFFOTgyQjBDNzIzOUNDRTA5MzkiIHN0UmVmOmRvY3VtZW50SUQ9InhtcC5kaWQ6ODRFQ0VBMUI2NzI2MTFFOTgyQjBDNzIzOUNDRTA5MzkiLz4gPC9yZGY6RGVzY3JpcHRpb24+IDwvcmRmOlJERj4gPC94OnhtcG1ldGE+IDw/eHBhY2tldCBlbmQ9InIiPz5W7JBiAAAA+ElEQVR42rTUsQrCMBAG4PjjA3To5uDm5is4uImP61IoOLg5d3UVOjj4CObgAhKa9C65BH4oSenHlfbfjOP4dM7tfC4+k2uzjj43nxcYo9z5oAVGz977HMCTfXz6BmjAejau4Nd4boDGGBkT+NAaXcToAH83WaFJLAYt0Cy2BNagq1gKLEFFWA7UoGJsDZSgKkwC5lA1Rmsr/PoCGoAH73caTDphjH4Z6vhajGlBk4WCnzpMFiZVlQMKG+TEUTcSKhqkqJFQWVdqFAZ1pUJR241aFAaYCoURJkZhiIlQGGOrKBpgWZTAoQGWQgcCZ593AyxGyZh/AgwAn7mVTH6QAL4AAAAASUVORK5CYII=");
    background-size: 100% 100%;
}
.prompt-input{
  margin: 8%;
  padding: 10rpx 15rpx;
  width: 80%;
  height:85rpx;
  border: 1px solid #ccc;
  border-radius: 10rpx;
}
.prompt-btn-group{
  width: 750rpx;
  height: 60rpx;
  line-height: 60rpx;
  text-align: center;
  background-color:#E73C2F;
}
.prompt-text{
	height: 500rpx;
	font-size:28rpx;
}
.content_text {
    line-height: 30rpx;
    margin: 30rpx;
}
</style>