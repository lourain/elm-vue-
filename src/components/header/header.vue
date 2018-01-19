<template>
	<div class="header" @click="test($event)">
		<div class="content-wrapper">
			<div class="avatar">
				<img :src="seller.avatar" alt="" width="64" height="64">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div v-if="seller.supports" class="support">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{seller.supports[0].description}}</span>
				</div>
			</div>
			<div class="support-count" v-if="seller.supports" @click="showDetail">
				<span class="count">{{seller.supports.length}}个</span>
				<i class="icon-keyboard_arrow_right"></i>
			</div>
		</div>
		<div class="bulletin-wrapper">
			<span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
			<i class="icon-keyboard_arrow_right"></i>
		</div>
		<div class="background">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>
		<transition name="fade">
			<div class="detail" v-show="detailShow">
				<div class="detail-wrapper clearfix">
					<div class="detail-main">
						<h1 class="name">{{seller.name}}</h1>
						<star :size="48" :score="seller.score" class="star-wrapper"></star>
						<div class="title">
							<div class="line"></div>
							<div class="text">优惠信息</div>
							<div class="line"></div>
						</div>
						<ul v-if="seller.supports" class="supports">
							<li class="supports-item" v-for="(item,index) in seller.supports" :key="index">
								<span class="icon" :class="classMap[seller.supports[index].type]"></span>
								<span class="text">{{seller.supports[index].description}}</span>
							</li>
						</ul>
						<div class="title">
							<div class="line"></div>
							<div class="text">商家信息</div>
							<div class="line"></div>
						</div>
						<div class="bulletin">
							<p class="content">{{seller.bulletin}}</p>
						</div>
					</div>
				</div>
				<div class="detail-close" @click="hideDetail">
					<i class="icon-close"></i>
				</div>
			</div>
		</transition>
	</div>
</template>
<script type="text/ecmascript-6">
	import star from '@/components/star/star'

	export default {
		data() {
			return {
				detailShow: false
			}
		},
		components: {
			star
		},
		props: {
			seller: {
				type: Object
			}
		},
		mounted() {
			this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special']
			console.log(this.seller.supports)
		},
		methods: {
			test($event) {
				console.log($event);
			},
			showDetail() {
				this.detailShow = true
			},
			hideDetail() {
				this.detailShow = false
			}
		}
	}
</script>
<style lang="stylus">
	@import "../../common/stylus/mixin"
	.header
		color #fff
		background-color rgba(7, 17, 27, .5)
		.content-wrapper
			position relative
			padding 24px 12px 18px 24px
			.avatar
				display inline-block
			.content
				display inline-block
				font-size 14px
				margin-left 16px
				.title
					margin 2px 0 8px 0
					.brand
						display inline-block
						vertical-align top
						width 30px
						height 18px
						bg-image('brand')
						background-size 30px 18px
						background-repeat no-repeat
					.name
						margin-left 6px
						line-height 18px
						font-weight bold
				.description
					margin-bottom 10px
					line-height 12px
					font-size 12px
				.supports
					.icon
						display inline-block
						width 12px
						height 12px
						margin-right 4px
						background-size 12px 12px
						background-repeat no-repeat
						&.decrease
							bg-image('decrease_1')
						&.discount
							bg-image('discount_1')
						&.guarantee
							bg-image('guarantee_1')nadouxihuan
						&.invoice
							bg-image('invoice_1')
						&.special
							bg-image('special_1')
				.text
					font-size 10px
					line-height 12px
			.support-count
				position absolute
				right 12px
				bottom 18px
				padding 0 8px
				height 24px
				line-height 24px
				border-radius 14px
				background rgba(0, 0, 0, .2)
				text-align center
				.count
					vertical-align top
					font-size 10px
				.icon-keyboard_arrow_right
					font-size 10px
					line-height 24px
					margin-left 2px
		.bulletin-wrapper
			height 28px
			line-height 28px
			padding 0 22px 0 12px
			white-space nowrap
			overflow hidden
			text-overflow ellipsis
			background-color rgba(7, 17, 27, 0.2)
			.bulletin-title
				display inline-block
				width 22px
				height 12px
				bg-image('bulletin')
				background-size 22px 12px
				background-repeat no-repeat
			.bulletin-text
				vertical-align top
				margin 0 4px
				font-size 10px
			.icon-keyboard_arrow_right
				position absolute
				font-size 10px
				right 12px
				top 8px
		.background
			position absolute
			top 0
			left 0
			width 100%
			height 108px
			z-index -1
			filter blur(10px)
		.detail
			position absolute
			box-sizing border-box
			z-index 100
			top 0
			left 0
			width 100%
			height 100%
			overflow auto
			background-color rgba(7, 17, 27, .8)
			&.fade-enter-active,fade-leave-active
				///*transition:  background-color .5s*/
				background-color rgba(7, 17, 27, .8)
			&.fade-enter,&.fade-leave-to
				background-color rgba(7, 17, 27, 0)
			.detail-wrapper
				min-height 100%
				overflow hidden
				backdrop-filter blur(10px)
				.detail-main
					margin-top 64px
					padding-bottom 64px
					.name
						line-height 16px
						text-align center
						font-size 16px
						font-weight 700
					.star-wrapper
						margin-top 18px
						padding 2px 0
						text-align center
		.title
			display flex
			width 80%
			margin 30px auto 24px auto
			.line
				flex: 1
				position: relative;
				top -6px
				border-bottom 1px solid rgba(255, 255, 255, .2)
			.text
				padding: 0 5px
		.supports
			width: 80%
			margin: 0 auto
			.supports-item
				padding: 0 12px
				margin-bottom 12px
				font-size: 10px
				&:last-child
					margin-bottom: 0;
				.icon
					display: inline-block
					width: 16px
					height: 16px
					vertical-align: top
					margin-right: 6px;
					background-size: 16px;
					background-repeat: no-repeat
					&.decrease
						bg-image('decrease_2')
					&.discount
						bg-image('discount_2')
					&.guarantee
						bg-image('guarantee_2')
					&.invoice
						bg-image('invoice_2')
					&.special
						bg-image('special_2')
				.text
					line-height: 12px
					font-size: 12px;
		.bulletin
			width: 80%
			margin: 0 auto
			.content
				padding: 0 12px
				line-height: 24px;
				font-size: 10px

	.detail-close
		position relative
		width 32px
		height 32px
		margin -64px auto 0
		clear both
		font-size 32px


</style>


