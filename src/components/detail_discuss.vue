<template>
	<div>
		<discuss-item :items="discuss.reviews"></discuss-item>
		<a class="more_comment" href="javascript:void(0)">全部影评{{discuss.total}}条</a>
	</div>
</template>
<script>
	import Api from '../assets/js/api'
	import discussItem from './discuss_item'
	export default{
		name:'short_discuss',
		components:{
			discussItem
		},
		data(){
			return {
				discuss:[]
			}
		},
		mounted(){
			this.getDiscuss();
		},
		methods:{
			getDiscuss(){
				var self=this;
				var movieId=this.$route.params.id;
        this.$http.jsonp(Api.url+'/v2/movie/subject/'+movieId+'/reviews?apikey=0b2bdeda43b5688921839c8ecb20399b&start=0&count=5').then(function(response){
          self.discuss=response.body;
        });
			}
		}
	}
</script>
<style>

</style>
