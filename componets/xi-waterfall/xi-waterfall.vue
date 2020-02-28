<template>
	<view class="container">
		<!-- 第一列 -->
		<view class="column" id="columnFirst">
			<view class="item" v-for="(item, index) in columnFirst" :key="index">
				<image :src="item.img" mode="widthFix"></image>
				<view>{{ item.title }}</view>
			</view>
		</view>
		<!-- 第二列 -->
		<view class="column" id="columnSecond">
			<view class="item" v-for="(item, index) in columnSecond" :key="index">
				<image :src="item.img" mode="widthFix"></image>
				<view>{{ item.title }}</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	props: {
		list: {
			type: Array,
			default: function() {
				return [];
			}
		}
	},
	data() {
		return {
			tempArray: [],
			columnFirst: [],
			columnSecond: []
		};
	},
	methods: {
		// 获取dom元素的高度
		getDomHeight(selector) {
			let query = uni.createSelectorQuery().in(this);
			let height = 0;
			query
				.select(selector)
				.fields(
					{
						size: true
					},
					data => {
						height = data.height;
					}
				)
				.exec();
			return height;
		},
		//新增数据
		insert() {
			//只有数组内有数据才执行
			if (this.tempArray.length > 0) {
				//获取每一列的高度
				let columnFirstHeight = this.getDomHeight('#columnFirst'),
					columnSecondHeight = this.getDomHeight('#columnSecond');
				//获取加入的数据
				console.log( this.tempArray)
				let data = this.tempArray.splice(0, 1);
				if (columnFirstHeight == columnSecondHeight || columnFirstHeight < columnSecondHeight) {
					//当高度相对,或第一列小于其他列,数据加入到第一列
					this.columnFirst.push(data[0]);
				} else {
					//数据加入到第二列
					this.columnSecond.push(data[0]);
				}
				this.$nextTick(() => {
					//当数据渲染完毕后,可以进行添加,知道临时数据被添加完毕
					this.insert();
				});
			}
		},
		//清除数组
		clear() {
			this.columnFirst = [];
			this.columnSecond = [];
		}
	},
	watch: {
		list(newVal, oldVal) {
			//当监听到,数据有变化时
			if (newVal.length === 0) {
				//清空数据
				this.clear();
			} else if (newVal.length > 0) {
				//赋值给临时数组
				this.tempArray = newVal.slice(oldVal.length);
				console.log(newVal.slice(oldVal.length))
				//新增数据
				this.insert();
			}
		}
	}
};
</script>

<style>
.container {
	width: 100%;
	display: flex;
	align-items: flex-start;
}
.container .column{
	flex:1;
}
.container .column .item image{
	width: 100%;
}
</style>
