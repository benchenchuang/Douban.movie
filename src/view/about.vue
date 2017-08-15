<template>
  <div>
    <div class="user_box">

    	<div class="user_header">
    		<router-link :to="{name:'setting'}" class="iconfont icon-setup"></router-link>

    		<div v-if="is_login" class="user_signin">
    			<img src="../assets/imgs/avatar.jpg">
    			<p>常州吴彦祖</p>
    		</div>

    		<div v-else class="user_signin" @click='is_login=true'>
    			<img src="../assets/imgs/signup.png">
    			<p>未登录</p>
    		</div>
    		
    	</div>

    	<div class="scan_box">
    		<div class="movie_tab">
    			<ul>
    				<li :class="{on:scan==1}" @click="scan=1">想看</li>
    				<li :class="{on:scan==2}" @click="scan=2">在看</li>
    				<li :class="{on:scan==3}" @click="scan=3">看过</li>
    				<li :class="{on:scan==4}" @click="scan=4">影评</li>
    				<li :class="{on:scan==5}" @click="scan=5">影人</li>
    			</ul>
    		</div>
    		<div class="scan_item">
    			<dl v-if="scan==1">暂无想看内容...</dl>
    			<dl v-if="scan==2">暂无在看内容...</dl>
    			<dl v-if="scan==3">暂无看过内容...</dl>
    			<dl v-if="scan==4">暂无影评内容...</dl>
    			<dl v-if="scan==5">暂无影人内容...</dl>
    		</div>
    	</div>


    </div>
  </div>
</template>
<script>
	export default{
		data(){
			return{
				is_login:false,
				scan:1
			}
		}
	}
</script>
<style>
	.user_header{
		position: relative;
		width: 100%;
		padding: 30px 0;
		border-bottom: 10px solid #f1f1f1;
	}
	.icon-setup{
		position: absolute;
		font-size: 22px;
		padding: 10px;
		color: #888;
		right: 10px;
		top: 10px;
	}
	.user_signin{
		text-align: center;
		font-size: 16px;
		line-height: 2;
		color: #666;
	}
	.user_signin img{
		width: 80px;
		height: 80px;
		border-radius: 50%;
	}
	.movie_tab{
    width:100%;
    height:40px;
  }
  .movie_tab ul{
    position: fixed;
    width:100%;
    height:40px;
    line-height:40px;
    overflow: hidden;
    background: #fff;
    border-bottom: 1px solid #f1f1f1;
    z-index: 2;
  }
  .movie_tab ul li{
    float: left;
    width:20%;
    text-align: center;
    font-size: 12px;
    color: #aaa;
  }
  .movie_tab ul li.on{
    color: #222;
    height:38px;
    border-bottom: 2px solid #474747;
  }
  .scan_item dl{
  	text-align: center;
  	font-size: 18px;
  	color: #888;
  	line-height: 4;
  }
</style>
