<template>
	<div>
    <search-bar></search-bar>
    <div class="tab_box relocate">
      <ul>
        <li :class="{on:hot}" @click="getMovies">正在热映</li>
        <li :class="{on:!hot}" @click="getSource">即将上映</li>
      </ul>
    </div>
		<div class="clearfix"></div>
		<keep-alive><movie-hot v-show="hot" :movies="movies"></movie-hot></keep-alive>
    <keep-alive><movie-hot v-show="!hot" :movies="sources"></movie-hot></keep-alive>
	</div>
</template>

<script>
	import Api from '../assets/js/api'
	import halfTab from '../components/half-tab'
  import movieHot from '../components/movie-list'
	import searchBar from '../components/search_bar'

  	export default {
    name: 'movieList',
    components:{
  		halfTab,
  		movieHot,
      searchBar
    },
    data () {
      return {
      	movies:[],
      	sources:[],
        hot:true
      }
    },
    mounted(){
    	this.getMovies();
    },
    methods:{
    	getMovies(){
    		var self=this;
    		this.hot=true;
        this.$http.jsonp(Api.url+'/v2/movie/in_theaters').then(function(response){
          self.movies=response.body.subjects;
        });
    	},
      getSource(){
        var self=this;
        this.hot=false;
        this.$http.jsonp(Api.url+'/v2/movie/coming_soon').then(function(response){
          self.sources=response.body.subjects;
        });
      },
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
.relocate ul{
  top:44px;
}
  .tab_box{
    width: 100%;
    height: 50px;
  }
  .tab_box ul{
    position: fixed;
    width: 100%;
    height: 50px;
    line-height: 50px;
    border-bottom: 1px solid #f1f1f1;
    background: #fff;
    z-index: 9;
  }
  .tab_box ul li{
    float: left;
    width: 50%;
    text-align: center;
    color: #888;
  }
  .tab_box ul li.on{
    color: #474747;
    border-bottom: 2px solid #666;
  }
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
