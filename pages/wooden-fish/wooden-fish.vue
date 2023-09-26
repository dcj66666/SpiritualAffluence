<template>
	<div class="fish-box">
		<Muyu v-if="data.status == 1" :count="data.gongde" @addCount="addgongde"></Muyu>
		<Qiuqian v-if="data.status==3"></Qiuqian>
		<Shaoxiang v-if="data.status == 2"></Shaoxiang>
		<Toutai v-if="data.status == 4"></Toutai>
		<div class="total">功德：{{ data.gongde }}</div>
		<div class="butBox">
			<img src="@/static/woodenfish/muyu.png" class="but" @click="changeTab(1)" />
			<img src="@/static/woodenfish/yinyue.png" class="but" @click="music" />
			<img src="@/static/woodenfish/shaoxiang.png" class="but" @click="changeTab(2)" />
			<img src="@/static/woodenfish/qiuqian.png" class="but" @click="changeTab(3)" />
			<img src="@/static/woodenfish/toutai.png" class="but" @click="changeTab(4)" />
		</div>
		<!--背景音乐大悲咒-->
		<audio id="music2">
			<source src="@/static/woodenfish/3.mp3" />
		</audio>
	</div>
</template>

<script>
	import Muyu from "./muyu.vue";
	import Qiuqian from "./qiuqian.vue";
	import Shaoxiang from "./shaoxiang.vue";
	import Toutai from "./toutai.vue";
	import {
		onMounted,
		reactive
	} from "vue";
	export default {
		name: "woodenFish",

		components: {
			Muyu,
			Qiuqian,
			Shaoxiang,
			Toutai
		},
		setup() {
			let data = reactive({
				music: 0,
				gongde: 0,
				status: 1,
			});
			onMounted(() => {
				//判断本地是否存有次数，有的话赋值给time，没有的话设为0
				if (uni.getStorageSync("muyutime") != null) {
					data.gongde = uni.getStorageSync("muyutime") * 1;
				} else {
					uni.setStorageSync("muyutime", 0);
				}
			});

			function addgongde() {
				data.gongde++
			}

			function music() {
				if (data.music == 0) {
					data.music = 1;
					var audio = document.getElementById("music2"); //自动的音乐
					audio.play();
				} else {
					data.music = 0;
					var audio = document.getElementById("music2"); //自动的音乐
					audio.pause(); //音乐停止
				}
			}

			function changeTab(tab) {
				data.status = tab;
			}
			return {
				data,
				music,
				changeTab,
				Muyu,
				Qiuqian,
				Shaoxiang,
				addgongde
			};
		},
	};
</script>

<style scoped>
	.fish-box {
		position: relative;
		width: 100%;
		height: 100vh;
		display: flex;
		/*水平垂直居中*/
		align-items: center;
		justify-content: center;
		background: #a08738;
	}

	.butBox {
		width: 100vw;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-wrap: wrap;
		position: absolute;
		bottom: 10px;
		left: 50%;
		transform: translate(-50%, 0);
	}

	.total {
		color: white;
		position: absolute;
		bottom: 300px;
		left: 50%;
		transform: translate(-50%, 0);
		font-size: 24px;
	}

	.but {
		width: 50px;
		height: 120px;
		margin: 0 30px;
		cursor: pointer;
	}

	.but:hover {
		width: 60px;
		height: 120px;
		margin: 0 25px;
	}

	.but:active {
		width: 50px;
		height: 120px;
		margin: 0 30px;
	}
</style>