<template>
	<view class="container">
		<uni-section title="基本信息" type="line">
			<view class="example">
				<uni-forms ref="groupForm" :rules="groupRules" :model="groupFormData" labelWidth="80px">
					<uni-forms-item label="群ID" required name="id">
						<uni-easyinput v-model="groupFormData.id" placeholder="请输入群ID" />
					</uni-forms-item>
					<uni-forms-item label="群名" required name="name">
						<uni-easyinput v-model="groupFormData.name" placeholder="请输入群名" />
					</uni-forms-item>
					
					<uni-forms-item label="群人数" required name="num">
						<uni-data-checkbox v-model="groupFormData.num" mode="tag" :localdata="groupLocaldata.textNum" />
					</uni-forms-item>
				
					<uni-forms-item label="群分类" required name="category">
						<uni-data-checkbox v-model="groupFormData.category" multiple mode="tag" :localdata="groupLocaldata.textCategory" />
					</uni-forms-item>
					
					<uni-forms-item label="组织" required name="org">
						<uni-easyinput v-model="groupFormData.org" placeholder="输入学校/公司/姓氏/名称" />
					</uni-forms-item>
									
					<uni-forms-item label="群位置" name="location">
						<uni-data-picker v-model="groupFormData.location" :localdata="groupLocaldata.textLocation" popup-title="选择城市">
						</uni-data-picker>
					</uni-forms-item>
					
					<uni-forms-item label="群标签" required name="tags" class="item-uni-tag">
						<view>
							<view v-for="(item, index) in groupLocaldata.textTags">
								<uni-tag :circle="true" :inverted="true" :text="item.text" type="primary" @click="setTagType"/>
							</view>
						</view>
					</uni-forms-item>
					
					<uni-forms-item label="群平台" required name="platform">
						<uni-data-checkbox v-model="groupFormData.platform" mode="tag" :localdata="groupLocaldata.textPlatform" />
					</uni-forms-item>
					
					<uni-forms-item label="群简介">
						<uni-easyinput type="textarea" v-model="groupFormData.introduction" placeholder="请输入群介绍" />
					</uni-forms-item>
			</uni-forms>
			<button type="primary" @click="submit('groupForm')">提交</button>
			
			<!-- 基础用法，不包含校验规则 -->
			<uni-forms ref="baseForm" :model="baseFormData" labelWidth="80px">
				<uni-forms-item label="群ID" required>
					<uni-easyinput v-model="baseFormData.name" placeholder="请输入群ID" />
				</uni-forms-item>
				<uni-forms-item label="年龄" required>
					<uni-easyinput v-model="baseFormData.age" placeholder="请输入年龄" />
				</uni-forms-item>
				<uni-forms-item label="性别" required>
					<uni-data-checkbox v-model="baseFormData.sex" :localdata="sexs" />
				</uni-forms-item>
				<uni-forms-item label="兴趣爱好" required>
					<uni-data-checkbox v-model="baseFormData.hobby" multiple :localdata="hobbys" />
				</uni-forms-item>
				<uni-forms-item label="自我介绍">
					<uni-easyinput type="textarea" v-model="baseFormData.introduction" placeholder="请输入自我介绍" />
					</uni-forms-item>
					<uni-forms-item label="日期时间">
						<uni-datetime-picker type="datetime" return-type="timestamp"
							v-model="baseFormData.datetimesingle" />
					</uni-forms-item>
					<uni-forms-item label="选择城市">
						<uni-data-picker v-model="baseFormData.city" :localdata="cityData" popup-title="选择城市">
						</uni-data-picker>
					</uni-forms-item>

					<uni-forms-item label="选择技能">
						<uni-data-select v-model="baseFormData.skills" :localdata="skillsRange" >
						</uni-data-select>
					</uni-forms-item>
				</uni-forms>
			</view>
		</uni-section>

		<uni-section title="对齐方式" type="line">
			<view class="example">
				<view class="segmented-control">
					<uni-segmented-control :current="current" :values="items" @clickItem="onClickItem"
						styleType="button">
					</uni-segmented-control>
				</view>
				<!-- 展示不同的排列方式 -->
				<uni-forms ref="baseForm" :modelValue="alignmentFormData" :label-position="alignment">
					<uni-forms-item label="姓名" required>
						<uni-easyinput v-model="baseFormData.name" placeholder="请输入姓名" />
					</uni-forms-item>
					<uni-forms-item label="年龄" required>
						<uni-easyinput v-model="baseFormData.age" placeholder="请输入年龄" />
					</uni-forms-item>
				</uni-forms>
			</view>
		</uni-section>

		<uni-section title="表单校验" type="line">
			<view class="example">
				<!-- 基础表单校验 -->
				<uni-forms ref="valiForm" :rules="rules" :model="valiFormData" labelWidth="80px">
					<uni-forms-item label="姓名" required name="name">
						<uni-easyinput v-model="valiFormData.name" placeholder="请输入姓名" />
					</uni-forms-item>
					<uni-forms-item label="年龄" required name="age">
						<uni-easyinput v-model="valiFormData.age" placeholder="请输入年龄" />
					</uni-forms-item>
					<uni-forms-item label="自我介绍">
						<uni-easyinput type="textarea" v-model="valiFormData.introduction" placeholder="请输入自我介绍" />
					</uni-forms-item>
				</uni-forms>
				<button type="primary" @click="submit('valiForm')">提交</button>
			</view>
		</uni-section>

		<uni-section title="自定义校验规则" type="line">
			<view class="example">
				<!-- 自定义表单校验 -->
				<uni-forms ref="customForm" :rules="customRules" labelWidth="80px" :modelValue="customFormData">
					<uni-forms-item label="姓名" required name="name">
						<uni-easyinput v-model="customFormData.name" placeholder="请输入姓名" />
					</uni-forms-item>
					<uni-forms-item label="年龄" required name="age">
						<uni-easyinput v-model="customFormData.age" placeholder="请输入年龄" />
					</uni-forms-item>
					<uni-forms-item label="兴趣爱好" required name="hobby">
						<uni-data-checkbox v-model="customFormData.hobby" multiple :localdata="hobbys" />
					</uni-forms-item>
				</uni-forms>
				<button type="primary" @click="submit('customForm')">提交</button>
			</view>
		</uni-section>


		<uni-section title="动态表单" type="line">
			<view class="example">
				<!-- 动态表单校验 -->
				<uni-forms ref="dynamicForm" :rules="dynamicRules" :model="dynamicFormData" labelWidth="80px">
					<uni-forms-item label="邮箱" required name="email">
						<uni-easyinput v-model="dynamicFormData.email" placeholder="请输入姓名" />
					</uni-forms-item>
					<uni-forms-item v-for="(item,index) in dynamicFormData.domains" :key="item.id"
						:label="item.label+' '+index" required :rules="item.rules" :name="['domains',index,'value']">
						<view class="form-item">
							<uni-easyinput v-model="dynamicFormData.domains[index].value" placeholder="请输入域名" />
							<button class="button" size="mini" type="default" @click="del(item.id)">删除</button>
						</view>
					</uni-forms-item>
				</uni-forms>
				<view class="button-group">
					<button type="primary" size="mini" @click="add">新增域名</button>
					<button type="primary" size="mini" @click="submit('dynamicForm')">提交</button>
				</view>
			</view>
		</uni-section>
	</view>
</template>

<script setup lang="ts">
import { reactive, ref } from "vue"

	const groupFormData = reactive({
		id: "",		//群id
		name: "",		//群名字
		num: [0],		//群人数
		category: [0],	//分类
		org: "",		//组织
		location: "",	//群位置
		tag: [0],		//群标签
		platform: "",	//群平台
		introduction: "",		//群简介
		screenshot: "",//群截图
		qrCode: "",	//二维码
		shareType: "",	//共享类型
		ownerId: "",	//群主或管理员联系方式
		service: "",	//客服联系方式
	})
	
	const groupRules = reactive({
			name: {
				rules: [{
					required: true,
					errorMessage: '姓名不能为空'
				}]
			},
			age: {
				rules: [{
					required: true,
					errorMessage: '年龄不能为空'
				}]
			},
			hobby: {
				rules: [{
						format: 'array'
					},
					{
						validateFunction: function(rule, value, data, callback) {
							if (value.length < 2) {
								callback('请至少勾选两个兴趣爱好')
							}
							return true
						}
					}
				]
			}
		})
	const groupLocaldata = reactive({
		textNum : [
			{
				text: '100人群',
				value: 1
			}, {
				text: '300人群',
				value: 2
			}, {
				text: '500人群',
				value: 3
			}, {
				text: '1000人群',
				value: 4
			}
		],
		textCategory: [
			{
				text: '宗亲群',
				value: 1
			},
			{
				text: '校友群',
				value: 2
			},
			{
				text: '同事群',
				value: 3
			},
			{
				text: '客户群',
				value: 4
			},
			{
				text: '老乡群',
				value: 5
			},
			{
				text: '其他群',
				value: 6
			}
		],
		textLocation : [
			{
				text: "广东省",
				value: "1-0",
				children: [{
						text: "深圳市",
						value: "1-1"
					},
					{
						text: "广州市",
						value: "1-2"
					}
				]
			},
			{
				text: "湖南省",
				value: "2-0",
				children: [{
						text: "长沙市",
						value: "2-1"
					},
					{
						text: "株洲市",
						value: "2-2"
					}
				]
			},
			{
				text: "四川省",
				value: "3-0",
				children: [{
						text: "成都市",
						value: "3-1"
					},
					{
						text: "绵阳市",
						value: "3-2"
					}
				]
			},
			{
				text: "湖北省",
				value: "3-0",
				disable: true
			}
		],
		textTags: [
			{
				text: '电商',
				value: 1
			},
			{
				text: '美妆',
				value: 2
			},
			{
				text: '同学',
				value: 3
			},
			{
				text: '宝妈',
				value: 4
			},
			{
				text: '同事',
				value: 5
			},
			{
				text: '化妆品',
				value: 6
			}
		],
		textPlatform : [
			{
				text: '微信群',
				value: 1
			}, {
				text: 'QQ群',
				value: 2
			}, {
				text: '抖音群',
				value: 3
			}, {
				text: '快手群',
				value: 4
			}, {
				text: 'WhatsApp群',
				value: 5
			}, {
				text: 'Line群',
				value: 6
			}, {
				text: 'TG群',
				value: 7
			}
		],
	})

// 基础表单数据
	const baseFormData = reactive({
		name: '',
		age: '',
		introduction: '',
		sex: 2,
		hobby: [5],
		datetimesingle: 1627529992399,
		city: '',
		skills: 0
	})
	const cityData = reactive([{
		text: "北京",
		value: "10001",
	}, {
		text: "上海",
		value: "10002",
	}, {
		text: "深圳",
		value: "10004",
	}])
	const skillsRange = reactive([{
			value: 0,
			text: "编程"
		},
		{
			value: 1,
			text: "绘画"
		},
		{
			value: 2,
			text: "运动"
		},
	])
	// 表单数据
	const alignmentFormData = reactive({
		name: '',
		age: '',
	})
	// 单选数据源
	const sexs = reactive([{
		text: '男',
		value: 0
	}, {
		text: '女',
		value: 1
	}, {
		text: '保密',
		value: 2
	}])
	// 多选数据源
	const hobbys = reactive([{
		text: '跑步',
		value: 0
	}, {
		text: '游泳',
		value: 1
	}, {
		text: '绘画',
		value: 2
	}, {
		text: '足球',
		value: 3
	}, {
		text: '篮球',
		value: 4
	}, {
		text: '其他',
		value: 5
	}])
	// 分段器数据
	const current = ref(0)
	const items = reactive( ['左对齐', '顶部对齐'])
	// 校验表单数据
	const valiFormData = reactive({
		name: '',
		age: '',
		introduction: '',
	})
	// 校验规则
	const rules = reactive({
		name: {
			rules: [{
				required: true,
				errorMessage: '姓名不能为空'
			}]
		},
		age: {
			rules: [{
				required: true,
				errorMessage: '年龄不能为空'
			}, {
				format: 'number',
				errorMessage: '年龄只能输入数字'
			}]
		}
	})
	// 自定义表单数据
	const customFormData = reactive({
		name: '',
		age: '',
		hobby: []
	})
	// 自定义表单校验规则
	const customRules = reactive({
		name: {
			rules: [{
				required: true,
				errorMessage: '姓名不能为空'
			}]
		},
		age: {
			rules: [{
				required: true,
				errorMessage: '年龄不能为空'
			}]
		},
		hobby: {
			rules: [{
					format: 'array'
				},
				{
					validateFunction: function(rule, value, data, callback) {
						if (value.length < 2) {
							callback('请至少勾选两个兴趣爱好')
						}
						return true
					}
				}
			]
		}
	
	})
	const dynamicFormData = reactive({
		email: '',
		domains: []
	})
	const dynamicLists = reactive([])
	const dynamicRules = reactive({
		email: {
			rules: [{
				required: true,
				errorMessage: '域名不能为空'
			}, {
				format: 'email',
				errorMessage: '域名格式错误'
			}]
		}
	})
	
	const setTagType = (e) => {
		console.log("setTagType---")
		console.log(e)
		// let types = ["default", "primary", "success", "warning", "error"];
		// let index = types.indexOf(this.type);
		// types.splice(index, 1);
		// let randomIndex = Math.floor(Math.random() * 4);
		// this.type = types[randomIndex];
	}
	
	const onClickItem = (e) => {
		console.log(e);
		this.current = e.currentIndex
	}
	const add = () => {
		this.dynamicFormData.domains.push({
			label: '域名',
			value: '',
			rules: [{
				'required': true,
				errorMessage: '域名项必填'
			}],
			id: Date.now()
		})
	}
	const del = (id) => {
		let index = this.dynamicLists.findIndex(v => v.id === id)
		this.dynamicLists.splice(index, 1)
	}
	const submit = (ref) => {
		console.log(this.baseFormData);
		this.$refs[ref].validate().then(res => {
			console.log('success', res);
			uni.showToast({
				title: `校验通过`
			})
		}).catch(err => {
			console.log('err', err);
		})
	}
</script>

<style lang="scss" scoped>
	.item-uni-tag {
		view {
			display: flex;
			flex-flow: row wrap;
			align-items: center;
			justify-content: space-between;
			margin-top: 7rpx;
		}
		
	}
	
	.example {
		padding: 15px;
		background-color: #fff;
	}

	.segmented-control {
		margin-bottom: 15px;
	}

	.button-group {
		margin-top: 15px;
		display: flex;
		justify-content: space-around;
	}

	.form-item {
		display: flex;
		align-items: center;
		flex: 1;
	}

	.button {
		display: flex;
		align-items: center;
		height: 35px;
		line-height: 35px;
		margin-left: 10px;
	}
</style>
