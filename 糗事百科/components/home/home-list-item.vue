<template>
	<view class="home-list-item u-f-ac u-f-jsb" hover-class="home-list-hover" @tap="open">
		<view class="u-f-ac home-list-item-l">
			<view v-if="item.icon" class="icon iconfont" :class="[`icon-${item.icon}`]"></view>
			{{ item.name }}
		</view>
		<view class=" home-list-item-r icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
export default {
	props: {
		item: Object,
		index: Number
	},
	methods: {
		open() {
			switch (this.item.clicktype) {
				case 'navigateTo':
					if (this.item.url) {
						uni.navigateTo({
							url: this.item.url
						});
					}
					break;
					case 'clear':
						uni.showModal({
							title: '提示',
							content: '是否要清除缓存?',
							cancelText: '取消',
							confirmText: '立刻清除',
							success: res => {
								if(res.confirm) {
									uni.clearStorage()
									uni.showToast({
										title: '清除缓存成功'
									});
								}
							}
						});
						break;
			}
		}
	}
};
</script>

<style lang="scss" scoped>
.home-list {
	.home-list-item {
		padding: 20rpx;
		border-top: 1rpx solid #f4f4f4;
		border-bottom: 1rpx solid #f4f4f4;
		.home-list-item-l {
			color: #333;
			.icon {
				margin-right: 10rpx;
			}
		}
		.home-list-item-r {
			color: #ccc;
		}
	}
}
.home-list-hover {
	background-color: #eee;
}
</style>
