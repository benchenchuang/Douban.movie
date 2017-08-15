<template>
  <div id="app">
  	<div class="goTop" @click='goTop'>↑</div>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app',
  methods:{
  	goTop(){
	    document.documentElement.scrollTop = document.body.scrollTop =0;
	  }
  }
}
</script>

<style>
	.goTop{
		position: fixed;
		right: 16px;
		bottom: 70px;
		width: 40px;
		height: 40px;
		line-height: 40px;
		border-radius: 50%;
		font-size: 16px;
		color: #fff;
		text-align: center;
		background: rgba(0,0,0,.5);
		z-index: 999;
	}
</style>
