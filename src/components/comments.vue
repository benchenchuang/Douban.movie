<template>
	<div>
		<detail-header :title="title"></detail-header>
		<h3 class="comment_title">短评 {{comments.total}} 条</h3>
		<comment-item :comments="comments.comments" v-infinite-scroll="getComments" infinite-scroll-distance="100"></comment-item>
	</div>
</template>
<script>
	import commentItem from './comment_item'
	import detailHeader from '../components/detail_header'
	import Api from '../assets/js/api'
	import Vue from 'vue';
	  //滚动
	import infiniteScroll from 'vue-infinite-scroll'
	Vue.use(infiniteScroll);
	export default{
		components:{
			detailHeader,
			commentItem
		},
		data(){
			return{
				title:'全部短评',
				comments:[],
				getAll:10
			}
		},
		mounted(){
			this.getComments();
		},
		methods:{
			getComments(){
				var self=this;
				var thisId=this.$route.params.id;
        this.$http.jsonp(Api.url+'/v2/movie/subject/'+thisId+'/comments?apikey=0b2bdeda43b5688921839c8ecb20399b&start=0&count='+self.getAll).then(function(response){
          self.comments=response.body;
          self.getAll+=10
        });
			}
		}

	}
</script>
<style>
	.comment_title{
		padding: 0 16px;
		font-size: 13px;
		color: #888;
		line-height: 3;
		border-bottom: 1px solid #f1f1f1;
	}
</style>
