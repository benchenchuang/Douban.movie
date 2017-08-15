<template>
	<div class="movie_content">
		<div v-if="!movies.length" class="load_tip">别着急，努力加载中...</div>
	  	<ul>
	  		<router-link tag="li" :to="{name:'detail',params:{id:movie.id}}" class="movie_item" v-for="movie in movies" :key="movie.id">
	  			<div class="pic">
	  				<img :src="movie.images.small">
	  			</div>
	  			<div class="movie_desc">
	  				<h3 class="title">{{movie.title}}</h3>
	  				<div class="star">
	  					<i class="iconfont icon-star on" v-for='star in onStar(movie.rating.stars)'></i>
	  					<i class="iconfont icon-star"  v-for='star in offStar(movie.rating.stars)'></i>
	  					<span>{{movie.rating.average}}</span>
	  				</div>
	  				<p class="txt" v-if="movie.directors.length">导演:<span v-for='doctor in movie.directors'> {{doctor.name}} </span> </p>
	  				<p class="txt" v-if="movie.casts.length>0">主演:<span v-for="cast in movie.casts"> {{cast.name}} </span> </p>
	  				<p class="scan">2133人看过</p>
	  			</div>
	  			<span class="get_sale" >预售</span>
	  		</router-link>
	  	</ul>
  	</div>
</template>

<script>
  	export default {
    name: 'movieList',
    props:['movies'],
    data () {
      return {
      }
    },
    methods:{
    	onStar(value){
    		return parseInt(value/10);
    	},
    	offStar(value){
    		return 5-parseInt(value/10);
    	}
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.load_tip{
	width: 100%;
	height: 100px;
	line-height: 100px;
	text-align: center;
	font-size: 15px;
	color: #888;
}
.movie_item{
	position: relative;
	width: 100%;
	padding: 16px;
	box-sizing: border-box;
	border-bottom: 1px solid #f1f1f1;
	overflow: hidden;
}
.movie_item .pic{
	float: left;
	width:88px;
}
.movie_desc{
	margin-left: 100px;
	margin-right: 60px;
}
.movie_desc .title{
	font-size: 16px;
	color: #474747;
}
.movie_desc .txt{
	font-size: 12px;
	color: #aaa;
}
.movie_desc .scan{
	font-size: 12px;
	color: #474747;
}
.get_sale{
	position: absolute;
	top: 50%;
	right: 26px;
	width: 50px;
	padding: 3px 0;
	text-align: center;
	color: #feb10c;
	font-size: 13px;
	border:1px solid #feb10c;
	border-radius: 4px;
	-webkit-transform: translateY(-50%);
	transform: translateY(-50%);
}
.star{
	font-size: 10px;
	color: #ccc;
}
.star span{
	margin-left:3px;
	font-size: 13px;
}
.star .on{
	color: #feb10c;
}
</style>
