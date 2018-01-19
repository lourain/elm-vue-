<template>
    <div v-show="food">

    </div>
</template>

<script>
	export default {
		name: "food",
        props:{
			food:{
				type:Object
            }
        }
	}
</script>

<style lang="stylus" scoped>
    .food
        position: fixed;
        left: 0
        top: 0
        bottom: 48px
        z-index 30
        width: 100%
        background-color: #fff;
</style>