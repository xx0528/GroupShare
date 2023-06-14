
 <template>
	<view>
		
		 <u--form
				labelPosition="left"
				label-width="140rpx"
				:model="groupInfo"
				:rules="rules"
				ref="form1"
		>
			<u-form-item label="群ID" prop="id" borderBottom>
				<u--input v-model="groupInfo.id" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群名字" prop="name" borderBottom>
				<u--input v-model="groupInfo.name" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群人数" prop="num" borderBottom>
				<u--input v-model.number="groupInfo.num" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群分类" prop="category" borderBottom>
				<u--input v-model="groupInfo.category" border="none"></u--input>
			</u-form-item>
			<u-form-item label="组织" prop="org" borderBottom>
				<u--input v-model="groupInfo.org" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群位置" prop="location" borderBottom>
				<u--input v-model="groupInfo.location" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群标签" prop="tag" borderBottom>
				<u--input v-model="groupInfo.tag" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群平台" prop="platform" borderBottom>
				<u--input v-model="groupInfo.platform" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群简介" prop="desc" borderBottom>
				<u--input v-model="groupInfo.desc" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群截图" prop="screenshot" borderBottom>
				<u--input v-model="groupInfo.screenshot" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群二维码" prop="qrCode" borderBottom>
				<u--input v-model="groupInfo.qrCode" border="none"></u--input>
			</u-form-item>
			<u-form-item label="共享类型" prop="shareType" borderBottom>
				<u--input v-model="groupInfo.shareType" border="none"></u--input>
			</u-form-item>
			<u-form-item label="群主微信" prop="ownerId" borderBottom>
				<u--input v-model="groupInfo.ownerId" border="none"></u--input>
			</u-form-item>
			<u-form-item label="客服微信" prop="service" borderBottom>
				<u--input v-model="groupInfo.service" border="none"></u--input>
			</u-form-item>
			
	<!-- 		<u-form-item
					label="性别"
					prop="userInfo.sex"
					borderBottom
					@click="showSex = true; hideKeyboard()"
					ref="item1"
			>
				<u--input
					v-model="model1.userInfo.sex"
					disabled
					disabledColor="#ffffff"
					placeholder="请选择性别"
					border="none"
				></u--input>
				<template #right>
					<u-icon
						name="arrow-right"
					></u-icon>
				</template>
			</u-form-item> -->
		</u--form>
		<u-action-sheet
				:show="showSex"
				:actions="actions"
				title="请选择性别"
				description="如果选择保密会报错"
				@close="showSex = false"
				@select="sexSelect"
		>
		</u-action-sheet>
	</view>
</template>

<script setup lang="ts">
	import { reactive, ref } from "vue"
	
	const showSex = ref(false)
	const model1 = reactive({
		userInfo: {
			name: 'uview-plus UI',
			sex: '',
		},
	})
	const groupInfo = reactive({
		id : "",		//群id
		name : "",		//群名字
		num : "",		//群人数
		category : 0,	//分类
		org : "",		//组织
		location : "",	//群位置
		tag : "",		//群标签
		platform : "",	//群平台
		desc : "",		//群简介
		screenshot : "",//群截图
		qrCode : "",	//二维码
		shareType : "",	//共享类型
		ownerId : "",	//群主或管理员联系方式
		service : "",	//客服联系方式
	})
	const actions = reactive([
		{
			name: '男',
		},
		{
			name: '女',
		},
		{
			name: '保密',
		},
	])
	
	const rules = reactive({
			'userInfo.name': {
				type: 'string',
				required: true,
				message: '请填写姓名',
				trigger: ['blur', 'change']
			},
			'userInfo.sex': {
				type: 'string',
				max: 1,
				required: true,
				message: '请选择男或女',
				trigger: ['blur', 'change']
			},
		})
		
	const radio = ref('')
	const switchVal= ref(false)
	
	const sexSelect = (e) => {
			model1.userInfo.sex = e.name
		}
	
</script>

<style lang="scss">
	.status_bar {
		height: var(--status-bar-height);
		width: 100%;
	}
</style>
