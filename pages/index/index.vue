<template>
	<view class="content">
		<!-- title -->
		<view class="title">
			Lambda Valid Code
		</view>
		<view>
            <navigator url="valid-code?mobile=18387214612">
				<button type="default">下一步</button>
			</navigator>
        </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 10px;
		height: 750upx;
		width: 750upx;
	}
	.title {
		font-size: 36upx;
		color: #8f8f94;
		margin-bottom: 50upx;
	}
</style>
