<template>
	<div id="app">
		<v-header :seller="seller"></v-header>
		<div class="tab border-1px">
			<router-link tag="div" class="tab-item" to="/goods">
				<a>商品</a>
			</router-link>
			<router-link tag="div" class="tab-item" to="/ratings">
				<a>评价</a>
			</router-link>
			<router-link tag="div" class="tab-item" to="/seller">
				<a>商家</a>
			</router-link>
		</div>
		<router-view :seller="seller"></router-view>
	</div>
</template>

<script type="text/ecmascript-6">
	import header from './components/header/header'
	import axios from 'axios'
	export default {
		components: {
			"v-header": header
		},
		data() {
			return {
				seller: {}
			}
		},
		created() {
			axios.get('../data.json').then((res) => {
				this.seller = res.data.seller
				console.log(res);
			})
		}
	}
</script>
<style lang="stylus">
	@import "./common/stylus/mixin.styl"
	.tab
		display flex
		height 40px
		line-height 40px
		border-1px(rgba(7, 17, 27, 0.1))
		.tab-item
			flex 1
			text-align center
			& > a
				color rgb(77, 85, 93)
				font-size 14px
				display block
			&.active > a
				color #f01414

</style>
