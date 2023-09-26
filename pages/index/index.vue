<template>
	<view class="content">
		<view class="head-box"></view>
		<view class="content-box">
			<view class="content-left-box">
				<view v-for="(item, index) in leftList" :key="index"
					:style="{ 'background-image': `url(${item.bgImage})` }" class="item-left-box"
					@click="urlTo(item.url)">
					<view>{{ item.title }}</view>
					<view>
						<view></view>
						<view></view>
					</view>
				</view>
			</view>
			<view class="content-right-box">
				<SpiSwitch></SpiSwitch>
				<view v-for="(item, index) in rightList" :key="index"
					:style="{ 'background-image': `url(${item.bgImage})` }" class="item-right-box"
					@click="urlTo(item.url)">
					<view>{{ item.title }}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import SpiSwitch from "@/components/SpiSwitch/SpiSwitch.vue";
	export default {
		components: {
			SpiSwitch,
		},
		data() {
			return {
				leftList: [{
						bgImage: "/static/7.jpg",
						url: "/pages/index2/index2",
						title: "drink",
					},
					{
						bgImage: "/static/4.jpg",
						url: "/pages/wooden-fish/wooden-fish",
						title: "woodenFish",
					},
					{
						bgImage: "/static/2.jpg",
						url: "",
					},
				],
				rightList: [{
						bgImage: "/static/3.jpg",
						url: "",
					},
					{
						bgImage: "/static/9.jpg",
						url: "",
					},
					{
						bgImage: "/static/7.jpg",
						url: "",
					},
				],
			};
		},
		onLoad() {},
		methods: {
			urlTo(url) {
				uni.navigateTo({
					url,
				});
			},
		},
	};
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.head-box {
		background-image: url(/static/6.jpg);
		width: 100vw;
		height: 600rpx;
	}

	.content-box {
		display: flex;
		justify-content: space-between;
		margin-top: 30rpx;
	}

	.content-left-box,
	.content-right-box {
		width: 50vw;
	}

	.item-left-box,
	.item-right-box {
		height: 300rpx;
		margin: 36rpx;
		border-radius: 10rpx;
	}

	.item-right-box {
		margin-left: 20rpx;
	}

	.item-left-box {
		margin-right: 20rpx;
	}
</style>