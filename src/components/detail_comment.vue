<template>
	<div>
		<comment-item :comments="comments.comments"></comment-item>
		<a class="more_comment" href="javascript:void(0)">全部短评{{comments.total}}条</a>
	</div>
</template>
<script>
	import Api from '../assets/js/api'
	import commentItem from './comment_item'
	export default{
		name:'short_discuss',
		data(){
			return {
				comments:[]
			}
		},
		components:{
			commentItem
		},
		mounted(){
			this.getComment();
		},
		methods:{
			getComment(){
				var self=this;
				var movieId=this.$route.params.id;
        this.$http.jsonp(Api.url+'/v2/movie/subject/'+movieId+'/comments?apikey=0b2bdeda43b5688921839c8ecb20399b&start=0&count=5').then(function(response){
          self.comments=response.body;
        });
			}
		}
	}
</script>
