<template>
	<div>
		<router-link tag='div' :to="{name:'discuss_detail',params:{id:item.id,content:item}}" class="discuss_item" v-for='item in items' :key='item.id'>
			<h3 class="discuss_title">{{item.title}}</h3>
			<div class="discuss_author">
				<span>{{item.author.name}}</span>
				<div class="star">
					<i class="iconfont icon-star on" v-for='star in onStar(item.rating.value)'></i>
					<i class="iconfont icon-star"  v-for='star in offStar(item.rating.value)'></i>
				</div>
			</div>
			<p class="discuss_summary">{{item.summary}}</p>
			<p class="more_info">{{item.useful_count}} / {{(item.useful_count)+(item.useless_count)}} 有用</p>
		</router-link>
	</div>
</template>
<script>
	export default{
		props:['items'],
		methods:{
			onStar(value){
    			return value;
	    	},
	    	offStar(value){
	    		return 5-value;
	    	}
		}
	}
</script>
<style>
	.discuss_item{
		padding:10px 16px;
	}
	.discuss_title{
		font-size: 16px;
		color: #474747;
	}
	.discuss_author{
		margin:5px 0;
		font-size: 12px;
		height: 24px;
		line-height: 24px;
		color: #aaa;
		overflow: hidden;
	}
	.discuss_author span,
	.discuss_author .star{
		display: inline-block;
	}
	.discuss_summary{
		font-size: 12px;
		color: #999;
	}
	.more_info{
		margin-top: 5px;
		font-size: 12px;
		color: #999;
	}
	.star{
		font-size: 10px;
		color: #ccc;
	}
	.star .on{
		color: #feb10c;
	}
</style>