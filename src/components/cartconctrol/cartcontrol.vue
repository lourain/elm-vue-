<template>
    <div class="cartconctrol">
        <transition name="move">
            <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click="decreaseCart"></div>
        </transition>
        <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
        <div class="cart-add icon-add_circle" @click="addCart"></div>
    </div>
</template>
<script type="text/ecmascript-6">
	import Vue from 'vue';

	export default {
		props: {
			food: {
				type: Object
			}
		},
		created() {
			// console.log(this.food);
		},
		methods: {
			addCart(event) {
				if (!event._constructed) {
					return false;
				}
				if (!this.food.count) {
					Vue.set(this.food, 'count', 1)
				} else {
					this.food.count++;
				}
				this.$emit('cartAdd',event.target);
			},
			decreaseCart() {
				if (!event._constructed) {
					return false;
				}
				if (this.food.count) {
					this.food.count--;
                }
			}
		}
	}
</script>
<style lang="stylus">
    .cartconctrol
        font-size: 0;
        .cart-decrease,.cart-add
            display inline-block
            padding 6px
            color darkgreen
            line-height: 24px;
            font-size: 24px
        .move-enter-active,.move-leave-active
            transition all .5s
        .move-enter,.move-leave-to
            opacity 0
            transform:translate3d(24px,0,0) rotate(360deg)
        .cart-count
            display inline-block
            vertical-align: top
            width: 12px
            padding-top: 6px
            line-height: 24px;
            text-align center
            font-size: 10px;

</style>