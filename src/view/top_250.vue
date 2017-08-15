<template>
	<div>
		<detail-header :title='title'></detail-header>
    <div class="movie_tab">
      <ul>
        <li @click="getTops(1,0)" :class="{on:start==1}">Top1-50</li>
        <li @click="getTops(2,50)" :class="{on:start==2}">51-100</li>
        <li @click="getTops(3,100)" :class="{on:start==3}">101-150</li>
        <li @click="getTops(4,150)" :class="{on:start==4}">151-200</li>
        <li @click="getTops(5,200)" :class="{on:start==5}">201-250</li>
      </ul>
    </div>
    <keep-alive><movie-item :items="movies.subjects" :start="movies.start"></movie-item></keep-alive>
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
        title:'豆瓣电影Top250',
				start:1,
			}
		},
		mounted(){
      this.$nextTick(function(){
            this.getTops(1,0,50)
			})
		},
		methods:{
			getTops(num,start,end){
				var self=this;
				this.start=num;
        this.movies=[];
        this.$http.jsonp(Api.url+'/v2/movie/top250?apikey=0b2bdeda43b5688921839c8ecb20399b&start='+start+'&count=50').then(function(response){
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
