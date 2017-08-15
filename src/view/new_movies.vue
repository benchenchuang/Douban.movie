<template>
	<div>
		<detail-header :title='title'></detail-header>
    <keep-alive><movie-item :items="movies.subjects" :start="start"></movie-item></keep-alive>
    <div v-if="!movies.subjects">
      <p class="loading">热情加载中，请耐心等待...</p>
    </div>
	</div>
</template>
<script>
	import Api from '../assets/js/api'
	import movieItem from '../components/movie_item'
	import detailHeader from '../components/detail_header'
	export default{
		components:{
			detailHeader,
			movieItem
		},
		data(){
			return{
				movies:[],
        title:'豆瓣电影新片榜',
				start:0,
			}
		},
		mounted(){
      this.$nextTick(function(){
            this.getNewMovies()
			})
		},
		methods:{
			getNewMovies(){
				var self=this;
        this.$http.jsonp(Api.url+'/v2/movie/new_movies?apikey=0b2bdeda43b5688921839c8ecb20399b').then(function(response){
          self.movies=response.body;
        });
			}
		}
	}
</script>
<style>
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
  .loading{
    margin-top: 60px;
    width:100%;
    text-align: center;
    font-size: 16px;
    color: #888;
    line-height:3px;
  }
</style>
