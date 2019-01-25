<template>
	<view>
		<view class="page uni-common-pb">
			<view class="message-tip">
				<view>验证码已经发送到您到手机</view> <view class="mobile">{{ mobile }}</view>
			</view>

			<view class="code-tip">
				<view class="left"> 6位数字验证码 </view>
				<view class="right">
					<button size="mini" type="primary" plain>重新获取</button>
				</view>
			</view>
			<view class="codes">
				<view v-for="item in config.count" :key="item.key">
					<view
						class="input"
						@tap="hanldeOpenKeyboard"
						:class="{ active: currentFocus == item.index }"
					>
						<template v-if="code[item.index - 1] != undefined">
							{{ code[item.index - 1] }}
						</template>
						<template v-else>
							<view v-if="currentFocus == item.index" class="shining"></view>
						</template>
					</view>
				</view>
			</view>
		</view>
		<NumberKeyboard
			:open="keyboardVisible"
			@number="inputCode"
			@delete="deleteCode"
			@close="keyboardVisible = false"
		></NumberKeyboard>
	</view>
</template>
<script>

import NumberKeyboard from './number-keyboard.vue';
export default {
	components: {
		NumberKeyboard
	},
	data() {
		return {
			config: {
				count: [
					{
						index: 1,
						key: 'valid-code-input-1'
					},
					{
						index: 2,
						key: 'valid-code-input-2'
					},
					{
						index: 3,
						key: 'valid-code-input-3'
					},
					{
						index: 4,
						key: 'valid-code-input-4'
					},
					{
						index: 5,
						key: 'valid-code-input-5'
					},
					{
						index: 6,
						key: 'valid-code-input-6'
					}
				]
			},
			keyboardVisible: true,
			currentFocus: 1,
			mobile: '',
			code: [],
			validCode: '',
			style: {
				inputWidth: '40upx',
				inputHeight: '100upx'
			}
		};
	},
	methods: {
		inputCode(e) {
			this.code[this.currentFocus - 1] = e;
			if (this.currentFocus == 6) {
				this.login();
			}
			if (this.currentFocus <= 6) {
				this.currentFocus++;
			}
		},
		login() {
			uni.showLoading({
				title:"登陆中"
			});
			var login = true;
			setTimeout(function(){
				if (status == 200) {
					//TODO 登陆成功逻辑
					uni.showToast({
						title:"这里写登陆成功的逻辑",
						icon:"none"
					});
				} else {
					uni.showToast({
						title: "这里写登陆失败的逻辑",
						icon : "none"
					})
					this.currentFocus = 1;
					this.code = [];
				}
			}, 1000);
		},
		deleteCode() {
			this.currentFocus--;
			this.code.splice(-1, 1);
		},
		hanldeOpenKeyboard() {
			this.keyboardVisible = true;
		},
		sendMessage() {
			//TODO 发送验证码业务逻辑
			uni.showToast({
				title: '验证码发送成功',
				icon : "none"
			});
		}
	},
	onReady() {},
	onShow() {},
	onLoad(options) {
		this.mobile = options.mobile;
		this.sendMessage();
	}
};
</script>

<style>
/* #ifdef  MP-WEIXIN*/

page {
	background: #ffffff !important;
}

/* #endif */
</style>

<style lang="scss" scoped>
page {
	background: #ffffff !important;
}

.page {
	height: auto;
	min-height: 100%;
	padding: 10px;
	box-sizing: border-box;
	.options {
		padding: 10px;
		margin-top: 20px;

		.option {
			margin-bottom: 10px;
		}
	}
	.message-tip {
		color: #666666;
		line-height: 30px;
	}
	.code-tip {
		margin-top: 100upx;
		height: 100upx;
		display: flex;
		justify-content: space-between;
		.left {
			color: #666666;
		}
		.right {
			button {
				color: #fa541c;
				border: 1px solid #fa541c;
				font-size: 12px;
				border-radius: 2px;
			}
		}
	}
	.codes {
		display: flex;
		justify-content: space-around;
		flex-direction: row;

		input {
			background: #ffffff;
			border: 1px solid #eeeeee;
			width: 100upx;
			height: 100upx;
			text-align: center;
		}
		.input {
			display: flex;
			justify-content: center;
			align-items: center;
			background: #ffffff;
			border: 1px solid #eeeeee;
			width: 100upx;
			height: 100upx;
			font-size: 50upx;
			font-weight: 500;
			color: #333333;
			.shining {
				border: 1px solid #fa541c;
				height: 60upx;
				animation: shining 1s linear infinite;
				/* 其它浏览器兼容性前缀 */
				-webkit-animation: shining 1s linear infinite;
				-moz-animation: shining 1s linear infinite;
				-ms-animation: shining 1s linear infinite;
				-o-animation: shining 1s linear infinite;
			}
		}
		.active {
			border: 1px solid #fa541c;
			caret-color: #fa541c;
		}
	}

	.oneline-codes {
		input {
			text-align: center;
		}
	}
	@-webkit-keyframes shining {
		0% {
			opacity: 1;
		}
		50% {
			opacity: 1;
		}
		50.01% {
			opacity: 0;
		}
		100% {
			opacity: 0;
		}
	}
}
</style>
