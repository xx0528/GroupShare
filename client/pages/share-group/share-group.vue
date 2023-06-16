
 <template>
	<view>
		
		 <u--form labelPosition="left" label-width="140rpx" :model="groupInfo" :rules="rules" ref="form1">
			<u-form-item label="群ID" prop="id" borderBottom>
				<u--input v-model="groupInfo.id" border="none" placeholder="输入群ID"></u--input>
			</u-form-item>
			<u-form-item label="群名字" prop="name" borderBottom>
				<u--input v-model="groupInfo.name" border="none" placeholder="输入群名字"></u--input>
			</u-form-item>
			<u-form-item label="群人数" prop="num" borderBottom ref="item2" >
				<u-radio-group v-model="groupInfo.num">
					<u-radio
						:customStyle="{marginRight: '16px'}"
						v-for="(item, index) in textCfg.groupNum"
						:key="index"
						shape="square"
						:label="item.name"
						:name="item.name"
					>
					</u-radio>
				</u-radio-group>
			</u-form-item>
			<u-form-item label="群分类" prop="category" borderBottom ref="item3" >
				<u-checkbox-group v-model="groupInfo.category" shape="square" @change="change" >
					<u-checkbox
						:customStyle="{marginRight: '16px'}"
						v-for="(item, index) in textCfg.groupCategory"
						:key="index"
						:label="item.name"
						:name="item.name"
					>
					</u-checkbox>
				</u-checkbox-group>
			</u-form-item>
			<u-form-item label="组织" prop="org" borderBottom>
				<u--input v-model="groupInfo.org" border="none" placeholder="输入学校/公司/姓氏名称"></u--input>
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
		
		<view class="u-page">
			<u-navbar
				title="表单"
				@leftClick="navigateBack"
				safeAreaInsetTop
				fixed
				placeholder
			></u-navbar>
			<view class="u-demo-block">
				<text class="u-demo-block__title">基础使用</text>
				<view class="u-demo-block__content">
					<!-- 注意，如果需要兼容微信小程序，最好通过setRules方法设置rules规则 -->
					<u--form
						labelPosition="left"
						:model="model1"
						ref="form1"
					>
						<u-form-item
							label="姓名"
							prop="userInfo.name"
							borderBottom
							ref="item1"
						>
							<u--input
								v-model="model1.userInfo.name"
								border="none"
								placeholder="姓名,只能为中文"
							></u--input>
						</u-form-item>
						<u-form-item
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
							<u-icon
								slot="right"
								name="arrow-right"
							></u-icon>
						</u-form-item>
						<u-form-item
							label="水果"
							prop="radiovalue1"
							borderBottom
							ref="item2"
						>
							<u-radio-group v-model="model1.radiovalue1">
								<u-radio
									:customStyle="{marginRight: '16px'}"
									v-for="(item, index) in radiolist1"
									:key="index"
									:label="item.name"
									:name="item.name"
								>
								</u-radio>
							</u-radio-group>
						</u-form-item>
						<u-form-item
							label="兴趣爱好"
							prop="checkboxValue1"
							borderBottom
							labelWidth="80"
							ref="item3"
						>
							<u-checkbox-group
								v-model="model1.checkboxValue1"
								shape="square"
								@change="change"
							>
								<u-checkbox
									:customStyle="{marginRight: '16px'}"
									v-for="(item, index) in checkboxList1"
									:key="index"
									:label="item.name"
									:name="item.name"
								>
								</u-checkbox>
							</u-checkbox-group>
						</u-form-item>
						<u-form-item
							label="简介"
							prop="intro"
							borderBottom
							ref="item3"
						>
							<u--textarea
								placeholder="不低于3个字"
								v-model="model1.intro"
								count
							></u--textarea>
						</u-form-item>
						<u-form-item
							label="住店时间"
							prop="hotel"
							labelWidth="80"
							borderBottom
							@click="showCalendar = true; hideKeyboard()"
						>
							<u--input
								v-model="model1.hotel"
								disabled
								disabledColor="#ffffff"
								placeholder="请选择住店和离店时间"
								border="none"
							></u--input>
							<u-icon
								slot="right"
								name="arrow-right"
							></u-icon>
						</u-form-item>
						<u-form-item
							label="验证码"
							prop="code"
							labelWidth="80"
							borderBottom
						>
							<u--input
								v-model="model1.code"
								border="none"
								placeholder="请填写验证码"
							></u--input>
							<u-button
								slot="right"
								@tap="getCode"
								:text="tips"
								type="success"
								size="mini"
								:disabled="disabled1"
							></u-button>
						</u-form-item>
						<u-form-item
							label="生日"
							prop="userInfo.birthday"
							borderBottom
							@click="showBirthday = true; hideKeyboard()"
							ref="item1"
						>
							<u--input
								v-model="model1.userInfo.birthday"
								disabled
								disabledColor="#ffffff"
								placeholder="请选择生日"
								border="none"
							></u--input>
							<u-icon
								slot="right"
								name="arrow-right"
							></u-icon>
						</u-form-item>
					</u--form>
					<u-button
						type="primary"
						text="提交"
						customStyle="margin-top: 50px"
						@click="submit"
					></u-button>
					<u-button
						type="error"
						text="重置"
						customStyle="margin-top: 10px"
						@click="reset"
					></u-button>
					<u-action-sheet
						:show="showSex"
						:actions="actions"
						title="请选择性别"
						description="如果选择保密会报错"
						@close="showSex = false"
						@select="sexSelect"
					>
					</u-action-sheet>
					<!-- <u-calendar
						:show="showCalendar"
						mode="range"
						@confirm="calendarConfirm"
						@close="calendarClose"
						startText="住店"
						endText="离店"
						confirmDisabledText="请选择离店日期"
						:formatter="formatter"
					></u-calendar> -->
					<u-code
						ref="uCode"
						@change="codeChange"
						seconds="20"
						@start="disabled1 = true"
						@end="disabled1 = false"
					></u-code>
					<!-- <u-datetime-picker
						:show="showBirthday"
						:value="birthday"
						mode="date"
						closeOnClickOverlay
						@confirm="birthdayConfirm"
						@cancel="birthdayClose"
						@close="birthdayClose"
					></u-datetime-picker> -->
				</view>
			</view>
		</view>
	</view>
</template>

<script setup lang="ts">
	import { reactive, ref } from "vue"
	
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
	
	const textCfg = reactive({
		groupNum : [
			{
				name: '100人群',
				disabled: false
			},
			{
				name: '300人群',
				disabled: false
			},
			{
				name: '500人群',
				disabled: false
			},
			{
				name: '1000人群',
				disabled: false
			}
		],
		groupCategory : [
			{
				name: '宗亲群',
				disabled: false
			},
			{
				name: '校友群',
				disabled: false
			},
			{
				name: '同事群',
				disabled: false
			},
			{
				name: '客户群',
				disabled: false
			},
			{
				name: '老乡群',
				disabled: false
			},
			{
				name: '其他群',
				disabled: false
			}
		],
	})
	
	const fileList1 = reactive([])
	const disabled1 = ref(false)
	const tips = ref('')
	const value = ref('')
	const showCalendar = ref(false)
	const showBirthday = ref(false)
	const model1 = reactive({
		userInfo: {
			name: '楼兰',
			sex: '',
			birthday: ''
		},
		radiovalue1: '苹果',
		checkboxValue1: [],
		intro: '',
		code: ''
	})
	const showSex = ref(false)
	const birthday = reactive(Number(new Date()))
	const actions = reactive([{
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
		'userInfo.name': [{
			type: 'string',
			required: true,
			message: '请填写姓名',
			trigger: ['blur', 'change']
		}, {
			// 此为同步验证，可以直接返回true或者false，如果是异步验证，稍微不同，见下方说明
			validator: (rule, value, callback) => {
				// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
				return uni.$u.test.chinese(value);
			},
			message: "姓名必须为中文",
			// 触发器可以同时用blur和change，二者之间用英文逗号隔开
			trigger: ["change", "blur"],
		}],
		code: {
			type: 'string',
			required: true,
			len: 4,
			message: '请填写4位验证码',
			trigger: ['blur']
		},
		'userInfo.sex': {
			type: 'string',
			max: 1,
			required: true,
			message: '请选择男或女',
			trigger: ['blur', 'change']
		},
		radiovalue1: {
			type: 'string',
			min: 1,
			max: 2,
			message: '橙子有毒',
			trigger: ['change']
		},
		checkboxValue1: {
			type: 'array',
			min: 2,
			required: true,
			message: '不能太宅，至少选两项',
			trigger: ['change']
		},
		intro: {
			type: 'string',
			min: 3,
			required: true,
			message: '不低于3个字',
			trigger: ['change']
		},
		hotel: {
			type: 'string',
			min: 2,
			required: true,
			message: '请选择住店时间',
			trigger: ['change']
		},
		'userInfo.birthday': {
			type: 'string',
			required: true,
			message: '请选择生日',
			trigger: ['change']
		},
	})
	const radiolist1 = reactive([{
			name: '苹果',
			disabled: false
		},
		{
			name: '香蕉',
			disabled: false
		},
		{
			name: '毒橙子',
			disabled: false
		}
	])
	const checkboxList1 = reactive([{
			name: '羽毛球',
			disabled: false
		},
		{
			name: '跑步',
			disabled: false
		},
		{
			name: '爬山',
			disabled: false
		}
	])

	
	const afterRead = (event) => {
		fileList1.push({
			url: event.file,
			status: 'uploading',
			message: '上传中'
		})
	}

	const groupChange = (n) => {
		// console.log('groupChange', n);
	}

	const radioChange = (n) => {
		// console.log('radioChange', n);
	}

	const navigateBack = () => {
		uni.navigateBack()
	}

	const sexSelect = (e) => {
		model1.userInfo.sex = e.name
		$refs.form1.validateField('userInfo.sex')
	}

	const change = (e) => {
		// console.log(e);
	}

	const formatter = (day) => {
		const d = new Date()
		let month = d.getMonth() + 1
		const date = d.getDate()
		if (day.month == month && day.day == date + 3) {
			day.bottomInfo = '有优惠'
			day.dot = true
		}
		return day
	}

	const calendarConfirm = (e) => {
		showCalendar.value = false
		model1.hotel = `${e[0]} / ${e[e.length - 1]}`
		$refs.form1.validateField('hotel')
	}

	const codeChange = (text) => {
		tips.value = text;
	}

	const getCode = () => {
		if ($refs.uCode.canGetCode) {
			// 模拟向后端请求验证码
			uni.showLoading({
				title: '正在获取验证码'
			})
			setTimeout(() => {
				uni.hideLoading();
				// 这里此提示会被start()方法中的提示覆盖
				uni.$u.toast('验证码已发送');
				// 通知验证码组件内部开始倒计时
				$refs.uCode.start();
			}, 2000);
		} else {
			uni.$u.toast('倒计时结束后再发送');
		}
	}

	const calendarClose = () => {
		showCalendar.value = false
		$refs.form1.validateField('hotel')
	}

	const birthdayClose = () => {
		showBirthday.value = false
		$refs.form1.validateField('userInfo.birthday')
	}

	const birthdayConfirm = (e) => {
		showBirthday.value = false
		model1.userInfo.birthday = uni.$u.timeFormat(e.value, 'yyyy-mm-dd')
		$refs.form1.validateField('userInfo.birthday')
	}

	const submit = () => {
		// 如果有错误，会在catch中返回报错信息数组，校验通过则在then中返回true
		$refs.form1.validate().then(res => {
			uni.$u.toast('校验通过')
		}).catch(errors => {
			uni.$u.toast('校验失败')
		})
	}

	const reset = () => {
		const validateList = ['userInfo.name', 'userInfo.sex', 'radiovalue1', 'checkboxValue1', 'intro',
		'hotel', 'code', 'userInfo.birthday']
		$refs.form1.resetFields()
		$refs.form1.clearValidate()
		setTimeout(()=>{
			$refs.form1.clearValidate(validateList)
			// 或者使用 $refs.form1.clearValidate()
		},10)
	}

	const hideKeyboard = () => {
		uni.hideKeyboard()
	}
	
	
</script>

<style lang="scss">
	.status_bar {
		height: var(--status-bar-height);
		width: 100%;
	}
</style>
