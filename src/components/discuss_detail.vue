<template>
	<div>
		<detail-header :title='title'></detail-header>
		<div class="discuss_box">
			<h2>{{data.title}}</h2>
			<div class="author">
				<div class="avatar fl"><img :src='data.author.avatar'></div>
				<div class="author_info">
					<p><span>{{data.author.name}} </span>的影评</p>
					<div>
						<span>{{(data.created_at).substr(0,10)}}</span>
						<div class="star" style="display:inline-block">
							<i class="iconfont icon-star on" v-for='star in onStar(data.rating.value)'></i>
							<i class="iconfont icon-star"  v-for='star in offStar(data.rating.value)'></i>
						</div>
					</div>
				</div>
			</div>
			<div class="discuss_content">
				<pre>{{data.content}}</pre>
			</div>
		</div>
	</div>
</template>
<script>
	import Api from '../assets/js/api'
	import detailHeader from './detail_header'
	export default{
		components:{
			detailHeader
		},
		data(){
			return{
				data:[],
				title:'影评'
			}
		},
		mounted(){
			this.getDeatail()
		},
		methods:{
			getDeatail(){
			  var self=this;
				var thisId=this.$route.params.id;
        this.$http.jsonp(Api.url+'/v2/movie/review/'+thisId+'?apikey=0b2bdeda43b5688921839c8ecb20399b').then(function(response){
          self.data=response.body;
        });

			},
			onStar(value){
    			return value;
      },
      offStar(value){
        return 5-value;
      }
		}
	}
</script>
<style scoped>
	.fl{
		float: left;
	}
	.discuss_box{
		padding: 20px;
    box-sizing: border-box;
	}
	.discuss_box h2{
		font-size: 18px;
		color: #333
	}
	.author{
		margin-top: 15px;
		overflow: hidden;
	}
	.avatar,
	.avatar img{
		width: 40px;
		height: 40px;
		border-radius: 50%;
	}
	.author_info{
		margin-left: 50px;
		font-size: 12px;
		color: #aaa;
	}
	.discuss_content{
		margin-top: 20px;
		font-size: 14px;
		line-height: 1.8;
		color: #666;
	}
	.discuss_content pre{
		display: block;
	  font-family: -moz-fixed;
	  white-space: pre-wrap;
	}
</style>
