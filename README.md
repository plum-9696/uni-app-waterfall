## 瀑布流组件
*在微信小程序和web页面已经使用了*
因为有个项目需要用到瀑布流布局,但是插件市场没有合适的组件,所以自己写了一个,因为非专业前端人员,代码有些的不好的地方,多多指教.
** 组件只做了大体的功能,每个item部分需要根据自己的样式做修改,组件只做了两列,可以根据自己情况,修改部分代码,代码都有注释应该很方便,如果有疑问或bug可以vx:ad19960906,或评论提出.**

瀑布流组件,兼容带图片的,每次插入数据会自动取算高度,只适用于固定列的,组件只做了两列,如果有多列可自行修改代码

如果有帮到你,可否帮忙点一个star [github地址](https://github.com/Joey-996/uni-app-waterfall "github")

## 使用方法
在 script 中引用组件
```
// 引入组件
import waterfall from '@/components/xi-waterfall/xi-waterfall.vue';
export default {
	components: { waterfall },
}
```
在template中使用组件
```
<waterfall></waterfall>
```
使用方法(2种)
* 绑定组件属性
组件会监听数组,进行瀑布流布局,比较通用
```
<waterfall :list='list'></waterfall>
```
* 使用方法
在模板添加ref属性
```
<waterfall ref="waterfall"><waterfall>
```
在script使用对应方法
```
//添加数据
this.$refs.waterfall.insert(data)
//清除数据
this.$refs.waterfall.clear()
```
## 组件的思路
* 给父容器添加两列子容器
* 每次插入数据的时候检测一下,比较两列高度
* 高度低的一列则插入数据,若高度一致则插入最左侧












