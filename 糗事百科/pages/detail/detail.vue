<template>
	<view>
		<detail-info :item="detail"></detail-info>
		<!-- 评论列表 -->
		<view class="u-comment-title">最新评论 {{ comment.count }}</view>
		<view class="uni-comment u-comment">
			<block v-for="(item, index) in comment.list" :key="index"><comment-list :item="item" :index="index"></comment-list></block>
		</view>
		<view style="height: 120rpx;"></view>
		<user-chat-bottom @submit="submit"></user-chat-bottom>
		<!-- 分享 -->
		<more-share :isShow="isShow" @toggle="toggle"></more-share>
	</view>
</template>

<script>
import detailInfo from '../../components/detail/detail-info.vue';
import commentList from "../../components/detail/comment-list.vue"
import time from "../../common/time.js"
import userChatBottom from "../../components/user-chat/user-chat-bottom.vue"
import moreShare from "../../components/common/more-share.vue"
export default {
	components: {
		detailInfo,
		commentList,
		userChatBottom,
		moreShare
	},
	data() {
		return {
			comment: {
				count: 20,
				list: []
			},
			detail: {
				userpic: '../../static/demo/userpic/14.jpg',
				username: '昵称',
				sex: 0, //0 男 1 女
				age: 20,
				isguanzhu: false,
				title: '我是标题',
				titlepic: '../../static/demo/datapic/13.jpg',
				morePic: ['../../static/demo/datapic/13.jpg', '../../static/demo/datapic/14.jpg', '../../static/demo/datapic/15.jpg'],
				video: false,
				share: false,
				path: '江苏 徐州',
				sharenum: 20,
				commentnum: 30,
				goodnum: 40
			},
			isShow: false
		};
	},
	methods: {
		// 初始化数据
		initData(obj) {
			// 设置标题
			uni.setNavigationBarTitle({
				title: obj.title
			});
		},
		// 获取评论
		getcomment() {
			let arr = [
				// 一级评论
				{
					id: 1,
					fid: 0,
					userpic: '../../static/demo/userpic/6.jpg',
					username: '小猫咪',
					time: '1555400035',
					data: '支持国产，支持DCloud!'
				},
				// 子级评论
				{
					id: 2,
					fid: 1,
					userpic: '../../static/demo/userpic/6.jpg',
					username: '小猫咪',
					time: '1555400035',
					data: '支持国产，支持DCloud!'
				},
				{
					id: 3,
					fid: 1,
					userpic: '../../static/demo/userpic/6.jpg',
					username: '小猫咪',
					time: '1555400035',
					data: '支持国产，支持DCloud!'
				},
				{
					id: 4,
					fid: 0,
					userpic: '../../static/demo/userpic/6.jpg',
					username: '小猫咪',
					time: '1555400035',
					data: '支持国产，支持DCloud!'
				}
			];
			for (let i = 0; i < arr.length; i++) {
				arr[i].time = time.gettime.gettime(arr[i].time);
			}
			this.comment.list = arr;
		},
		submit(data) {
			let obj = {
					id: 1,
					fid: 0,
					userpic: '../../static/demo/userpic/6.jpg',
					username: '小猫咪',
					time: time.gettime.gettime(new Date().getTime()),
					data: data
				}
				this.comment.list.push(obj)
			console.log(data)
		},
		toggle() {
			this.isShow = !this.isShow
		}
	},
	onLoad(e) {
		this.initData(JSON.parse(e.detailData));
		this.getcomment();
	},
	onNavigationBarButtonTap(e) {
		if (e.index == 0) {
			this.isShow = true
		}
	}
};
</script>

<style lang="scss">
.u-comment {
	padding: 0 20upx;
}
.u-comment-title {
	padding: 20upx;
	font-size: 30upx;
	font-weight: bold;
}
</style>
