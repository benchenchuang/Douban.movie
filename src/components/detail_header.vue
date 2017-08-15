<template>
	<div class="movie_header">
		<div class="header_box">
			<i class="iconfont icon-left" @click='goBack'></i>
			<h3>{{title}}</h3>
		</div>
	</div>
</template>
<script>
	export default{
		props:['title'],
		methods:{
			goBack(){
				window.history.back(-1);
			}
		}
	}
</script>
<style scoped>
	.movie_header{
		width: 100%;
		height: 44px;
	}
	.header_box{
		position: fixed;
		width: 100%;
		left: 0;
		top: 0;
		height: 44px;
		line-height: 44px;
		text-align: center;
		color: #fff;
		background: #4f4f4f;
		z-index: 3;
	}
	.header_box .iconfont{
		position: absolute;
		left: 16px;
		top: 0;
	}
	.header_box h3{
		font-size: 16px;
	}
</style>