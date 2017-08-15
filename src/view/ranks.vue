<template>
	<div>
		<search-bar></search-bar>
		<div class="rank_box">
			<h3 class="rank_title">精选榜单</h3>
			<router-link tag='div' :to="{name:'top250'}" class="rank_item top250">
				<div class="desc"><h2 class="name">{{sliceHead(top250.title)}}</h2> <span class="brief">8分以上好电影</span></div>
				<div class="rank_img">
					<img v-for='item in topThree(top250.subjects)' :src="item.images.small">
				</div>
			</router-link>
			<router-link tag='div' :to="{name:'weekly'}" class="rank_item weekly">
				<div class="desc"><h2 class="name">{{sliceHead(weekly.title)}}</h2> <span class="brief">{{usBox.date}}</span></div>
				<div class="rank_img">
					<img v-for='movie in topThree(weekly.subjects)' :src="movie.subject.images.small">
				</div>
			</router-link>
			<router-link tag='div' :to="{name:'new'}" class="rank_item new_movie">
				<div class="desc"><h2 class="name">{{sliceHead(newMovies.title)}}</h2> <span class="brief">{{usBox.date}}</span></div>
				<div class="rank_img">
					<img v-for='item in topThree(newMovies.subjects)' :src="item.images.small">
				</div>
			</router-link>

			<router-link tag='div' :to="{name:'us_box'}" class="rank_item us_box">
				<div class="desc"><h2 class="name">{{sliceHead(usBox.title)}}</h2> <span class="brief">{{usBox.date}}</span></div>
				<div class="rank_img">
					<img v-for='item in topThree(usBox.subjects)' :src="item.subject.images.small">
				</div>
			</router-link>
		</div>
    
  </div>
</template>
<script>
	import Api from '../assets/js/api'
	import searchBar from '../components/search_bar'
	export default{
		components:{
			searchBar
		},
		data(){
			return{
				top250:[],
				weekly:[],
				newMovies:[],
				usBox:[]
			}
		},
		mounted(){
			this.$nextTick(function(){
				this.getTops();
				this.getWeekly();
				this.getNewMovies();
				this.getUsBox();
			})
		},
		methods:{
			getTops(){//top250
				var self=this;
        this.$http.jsonp(Api.url+'/v2/movie/top250?apikey=0b2bdeda43b5688921839c8ecb20399b').then(function(response){
          self.top250=response.body;
        });
			},
			getWeekly(){//口碑榜
				var self=this;
        this.$http.jsonp(Api.url+'/v2/movie/weekly?apikey=0b2bdeda43b5688921839c8ecb20399b').then(function(response){
          self.weekly=response.body;
        });
			},
			getNewMovies(){//新片榜
				var self=this;
        this.$http.jsonp(Api.url+'/v2/movie/new_movies?apikey=0b2bdeda43b5688921839c8ecb20399b').then(function(response){
          self.newMovies=response.body;
        });
			},
			getUsBox(){//北美票房榜
				var self=this;
        this.$http.jsonp(Api.url+'/v2/movie/us_box?apikey=0b2bdeda43b5688921839c8ecb20399b').then(function(response){
          self.usBox=response.body;
        });
			},
			topThree(value){
				return value.slice(0,3)
			},
			sliceHead(value){
				return value.slice(4)
			}
		}
	}
</script>
<style>
	.rank_title{
		font-size: 18px;
		color: #474747;
		line-height: 2;
	}
	.rank_box{
		padding: 20px;
	}
	.rank_item{
		margin-top: 15px;
	    height: 130px;
	    border-radius: 10px;
	    color: #fff;
	}
	.top250{
		background: linear-gradient(#e1a708,#efd491);
	}
	.weekly{
		background: linear-gradient(#32c05e,#a1e5be);
	}
	.new_movie{
		background: linear-gradient(#a361c3,#d9b9e8);
	}
	.us_box{
		background: linear-gradient(#dd7286,#f3b9c5);
	}
	.rank_item .desc{
		vertical-align: top;
	    display: inline-block;
	    box-sizing: border-box;
	    padding-top: 50px;
	    width: 40%;
	    height: 100%;
    font-size: 12px;
	    text-align: center;
	}
	.rank_item .desc .name{
		font-size: 18px;
	}
	.rank_item .rank_img{
		  vertical-align: top;
	    display: inline-block;
	    width: 55%;
      max-width:210px;
	    height: 100%;
	    text-align: center;
	}
	.rank_img img{
		display: inline-block;
	    vertical-align: text-top;
	    position: relative;
	    top: 50%;
	    -webkit-transform: translateY(-50%);
	    transform: translateY(-50%);
	    width: 28%;
	}
	.rank_img img:nth-child(2){
		width: 35%;
	}
</style>
