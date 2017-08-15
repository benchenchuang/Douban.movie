<template>
	<div>
		<div v-for="comment in comments" class="comment_item">
			<div class="comment_user">
				<img :src="comment.author.avatar">
			</div>
			<div class="comment_content">
				<div class="comment_author">
					<span class="name">{{comment.author.name}}</span>
					<div class="star">
						<i class="iconfont icon-star on" v-for='star in onStar(comment.rating.value)'></i>
  						<i class="iconfont icon-star"  v-for='star in offStar(comment.rating.value)'></i>
					</div>
					<div class="zan" :class="{select:comment.is_zan}" @click="thumb(comment)"><i class="iconfont icon-zan"></i><span> {{comment.useful_count}}</span></div>
				</div>
				<div class="comment_txt">
					<p>{{comment.content}}</p>
				</div>
				<p class="comment_time">{{comment.created_at}}</p>
			</div>
		</div>
	</div>
</template>
<script>
	export default{
		props:['comments'],
		data(){
			return{
			}
		},
		methods:{
			onStar(value){
    			return value;
	    	},
	    	offStar(value){
	    		return 5-value;
	    	},
	    	thumb(item){
	    		item.is_zan=!item.is_zan;
	    		if(item.is_zan){
	    			item.useful_count+=1;
	    		}else{
	    			item.useful_count-=1;
	    		}
	    	}
		}
	}
</script>
<style>
	.select .iconfont,
	.select span{
		color: #feb10c
	}
	.comment_item{
		padding: 10px 16px;
		overflow: hidden;
	}
	.comment_item .comment_user{
		float: left;
	}
	.comment_user img{
		width: 30px;
		height: 30px;
		border-radius: 50%;
	}
	.comment_content{
		margin-left: 40px;
	}
	.comment_author{
		height: 24px;
		line-height: 24px;
		overflow: hidden;
	}
	.comment_author .name{
		float: left;
		max-width: 40%;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		font-size: 14px;
		color: #333;
	}
	.comment_author .star{
		float: left;
		margin-left:10px;
	}
	.comment_author .zan{
		float: right;
		color: #aaa;
		font-size: 12px;
	}
	.star .iconfont{
		color: #ddd;
	}
	.star .iconfont.on{
		color: #feb10c;
	}
	.comment_txt{
		margin:5px 0;
		font-size: 14px;
		color: #666;
	}
	.comment_time{
		font-size: 12px;
		color: #aaa;
	}
	.select{
		color: #feb10c
	}
</style>