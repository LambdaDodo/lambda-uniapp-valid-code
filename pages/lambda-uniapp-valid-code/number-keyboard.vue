<template>
	<view id="number-keyboard-component" class="numberkeyboard" v-show="numberKeyboardPopupVisible">
		<view class="title" @tap="close"> 
		 <image src="../../static/lambda-uniapp-valid-code/down.png" style="width: 30upx;height: 30upx;"></image>
		 </view>
		<view class="keys">
			<view class="key button" v-for="num in config.loop" :key="num.key" @tap="number(num.number)">{{num.number}}</view>
			<view class="key button" style="background: #eeeeee;"></view>
			<view class="key button" @tap="number(0)">0</view>
			<view class="key button" @tap="del" style="background: #eeeeee;">
				<image src="../../static/lambda-uniapp-valid-code/delete.png" style="width: 50upx;height: 50upx;"></image>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: 'number-keyboard',
	props: {
		open: {
			type: Boolean,
			default: false
		},
		color: {
			type: String,
			default: '#04BE02'
		}
	},

	data() {
		return {
			config :{
				loop : [
					{
						number : 1,
						key : 'number-1',
					},
					{
						number : 2,
						key : 'number-2',
					},
					{
						number : 3,
						key : 'number-3',
					},
					{
						number : 4,
						key : 'number-4',
					},
					{
						number : 5,
						key : 'number-5',
					},
					{
						number : 6,
						key : 'number-6',
					},
					{
						number : 7,
						key : 'number-7',
					},
					{
						number : 8,
						key : 'number-8',
					},
					{
						number : 9,
						key : 'number-9',
					},
				]
			},
			numberKeyboardPopupVisible: this.open
		};
	},
	watch: {
		numberKeyboardPopupVisible: function(value, oldValue) {
			if (value == false) {
				this.$emit('close');
			}
		},
		open: function(value, oldValue) {
			console.log(value);
			this.numberKeyboardPopupVisible = value;
		}
	},
	methods: {
		close(){
			this.numberKeyboardPopupVisible = false;
			this.$emit("close");
		},
		del() {
			this.$emit("delete");
		},
		number(number) {
			this.$emit("number", number);
		}
	}
};
</script>

<style scoped="scoped" lang="scss">
#number-keyboard-component {
	position: fixed;
	width: 100%;
	bottom: 0;

	.title {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 60upx;
		background: #eeeeee;
	}
	.keys {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;

		.key {
			width: 250upx;
			height: 100upx;
			display: flex;
			justify-content: center;
			align-items: center;
			border-right: 1px solid #eeeeee;
			box-sizing: border-box;
			font-size: 40upx;
			
		}
		.key:nth-child(n + 4) {
			border-top: 1px solid #eeeeee;
			box-sizing: border-box;
		}
		.key:active {
			background: #dddddd;
		}
	}

	.container {
		width: 100%;

		.count-text {
			justify-content: center;
			align-items: center;
			display: flex;
			/*height: 100px;*/
			/*background: #eee;*/
			font-size: 18px;
		}
	}
	.numberkeyboard-popup {
		width: 100%;
		z-index: 10;
		.count-text {
			position: fixed;
			top: -100px;
			font-size: 28px;
			color: #ffffff;
			width: 100%;
			text-align: center;
			font-weight: 500;
			span {
				padding: 0 40px;
				border-radius: 30px;
				background: -webkit-linear-gradient(left top, #999999, #777777);
			}
		}
		.desc-text {
			position: fixed;
			top: -40px;
			font-size: 12px;
			color: #ffffff;
			width: 100%;
			text-align: center;
			font-weight: 100;
		}
		.number {
			height: 70px;
			line-height: 70px;
			font-size: 25px;
			font-weight: 400;
			color: #666666;
			border-right: 1px solid #999999;
			box-sizing: border-box;
		}
		.number:nth-child(n + 4) {
			border-top: 1px solid #999999;
			box-sizing: border-box;
		}
		.number:active {
			background: #04be02;
			color: #ffffff;
			border: 0px solid #000000;
			box-shadow: 0 0 2px 2px #09bb07;
			box-sizing: border-box;
		}
		.number[data-value='.'] {
			font-weight: 900;
			font-size: 30px;
		}
		.del {
			height: 140px;
			vertical-align: middle;
			line-height: 140px;
			border-bottom: 0.1px solid #999999;
			box-sizing: border-box;
		}
		.del i {
			font-size: 35px;
			color: #666666;
		}
		.confirm {
			font-size: 15px;
			height: 140px;
			line-height: 140px;
			color: #ffffff;
		}
	}
}
</style>
