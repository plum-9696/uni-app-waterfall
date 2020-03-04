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
			columnSecond: [],
			columnFirstHeight: 0,
			columnSecondHeight: 0
		};
	},
	methods: {
		// 获取dom元素的高度
		async getDomHeight(selector) {
			return new Promise(resolve => {
				let query = uni.createSelectorQuery().in(this);
				query
					.select(selector)
					.fields(
						{
							size: true
						},
						data => {
							resolve(data.height);
						}
					)
					.exec();
			});
		},
		//新增数据
		async insert() {
			//只有数组内有数据才执行
			if (this.tempArray.length > 0) {
				//获取每一列的高度
				let columnFirstHeight = await this.getDomHeight('#columnFirst');
				let columnSecondHeight = await this.getDomHeight('#columnSecond');
				//获取加入的数据
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
		},
		//外部调用,添加数据
		insertData(data) {
			this.tempArray = data;
			//新增数据
			this.insert();
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
.container .column {
	flex: 1;
}
.container .column .item image {
	width: 100%;
}
</style>
