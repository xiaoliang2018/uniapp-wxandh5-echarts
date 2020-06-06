<template>
	<view class="content">
		<view style="height:400upx;width:100%">
			<mpvue-echarts class="ec-canvas" @onInit="lineInit" canvasId="line1" ref="lineChart" />
			<mpvue-echarts class="ec-canvas" @onInit="lineInit2" canvasId="line2" ref="lineChart2" />
		</view>
		<button type="default" @click="toggleData">切换</button>
	</view>
</template>

<script>
	// import * as echarts from '@/components/echarts/echarts.simple.min.js';
	import * as echarts from '@/components/echarts/echarts.min.js';
	// import  echarts from '@/components/echarts/echarts.min.dingzhi.js';
	
	import mpvueEcharts from '@/components/mpvue-echarts/src/echarts.vue';

	export default {
		data() {
			return {
				lineChart:'',
				// echarts: echarts,
			}
		},
		onLoad() {

		},
		components: {
			mpvueEcharts
		},
		methods: {
			lineOption(data = [120, 200, 150, 80, 70, 110, 130]){
				let lineOption = {
					tooltip: {
						trigger: 'item',
						formatter: '{a} \n{b}: {c} ({d}%)'
					},
					legend: {
						orient: 'vertical',
						left: 10,
						data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎']
					},
					series: [
						{
							name: '访问来源',
							type: 'pie',
							radius: ['50%', '70%'],
							avoidLabelOverlap: false,
							label: {
								show: false,
								position: 'center'
							},
							emphasis: {
								label: {
									show: true,
									fontSize: '10',
									fontWeight: 'bold'
								}
							},
							labelLine: {
								show: false
							},
							data: [
								{value: 335, name: '直接访问'},
								{value: 310, name: '邮件营销'},
								{value: 234, name: '联盟广告'},
								{value: 135, name: '视频广告'},
								{value: 1548, name: '搜索引擎'}
							]
						}
					]
				};
				return lineOption;
			},
			toggleData(){
				this.lineInit2({height: 200,width: 375.20001220703125},[111, 222, 333, 444, 555, 666, 777])
			},
			lineInit(e) {
				setTimeout(()=>{
					let {
						width,
						height
					} = e;
					let canvas = this.$refs.lineChart.canvas;
					echarts.setCanvasCreator(() => canvas);
					let lineChart = echarts.init(canvas, null, {
						width: width,
						height: height
					});
					canvas.setChart(lineChart);
					console.log(11)
					lineChart.setOption(this.lineOption([111, 222, 333, 444, 555, 666, 777]));
					this.$refs.lineChart.setChart(lineChart);
				},3000)

			},
			lineInit2(e,data){
				let {
					width,
					height
				} = e;
				console.log(e,'eeeeeeeeee')
				let canvas = this.$refs.lineChart2.canvas;
				echarts.setCanvasCreator(() => canvas);
				let lineChart2 = echarts.init(canvas, null, {
					width: width,
					height: height
				});
				canvas.setChart(lineChart2);
				
				if(data != undefined){
					lineChart2.setOption(this.lineOption(data));
				}else{
					lineChart2.setOption(this.lineOption());
				}
				this.$refs.lineChart2.setChart(lineChart2);
			}
		},
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
