<template>
	<view class="content">
		<button @tap="insertData">添加数据</button>
		<button @tap="list=[]">清空数据</button>
		<view style="width: 100%;">
			<waterfall :list="list"></waterfall>
		</view>
		
	</view>
</template>

<script>
// 引入组件
import waterfall from '@/components/xi-waterfall/xi-waterfall.vue';
export default {
	components: { waterfall },
	data() {
		return {
			list: [],
			//模拟数据
			data: [
				{
					title: '标题1',
					img: 'https://s2.ax1x.com/2020/02/28/3Dn6c8.png'
				},
				{
					title: '标题2',
					img: 'https://s2.ax1x.com/2020/02/28/3DntXD.jpg'
				},
				{
					title: '标题3',
					img: 'https://s2.ax1x.com/2020/02/28/3Dna0H.jpg'
				},
				{
					title: '标题4',
					img: 'https://s2.ax1x.com/2020/02/28/3Dn0AA.jpg'
				},
				{
					title: '标题5',
					img: 'https://s2.ax1x.com/2020/02/28/3DnRBQ.jpg'
				},
				{
					title: '标题6',
					img: 'https://s2.ax1x.com/2020/02/28/3Dns9P.jpg'
				},
				{
					title: '标题7',
					img: 'https://s2.ax1x.com/2020/02/28/3DncjS.jpg'
				},
				{
					title: '标题8',
					img: 'https://s2.ax1x.com/2020/02/28/3Dn2ng.jpg'
				}
			]
		};
	},
	methods: {
		insertData() {
			this.list = this.list.concat(this.data);
		}
	}
};
</script>

<style>
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
</style>
