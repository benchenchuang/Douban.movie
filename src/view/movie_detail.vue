<template>
	<div>
		<detail-header :title="detail.title" v-if='is_nav'></detail-header>

    <div v-if="!detail.images">
      <p class="loading">热情加载中，请耐心等待...</p>
    </div>

		<div class="movie_box" v-else>
			<div class="detail_pic">
				<img :src="detail.images.large">
			</div>
			<div class="detail_top">
				<div class="detail_grade">
					<p>豆瓣评分</p>
					<p class="grade_num">{{detail.rating.average}}</p>
					<div class="star">
						<i class="iconfont icon-star on" v-for='star in onStar(detail.rating.stars)'></i>
		  				<i class="iconfont icon-star"  v-for='star in offStar(detail.rating.stars)'></i>
		  			</div>
		  			<p>{{detail.ratings_count}}人</p>
				</div>
				<div class="detail_title">
					<h2>{{detail.title}}</h2>
					<div class="detail_txt">
						<p>{{detail.year}} / {{detail.countries[0]}} <span v-for='genere in detail.genres'> / {{genere}} </span></p>
						<p>上映日期: {{detail.year}}(中国大陆)</p>
					</div>
				</div>
			</div>

			<div class="detai_content">
				<h3 class="detail_h">剧情简介</h3>
				<p class="detail_desc">{{summary}}<a href="javascript:void(0)" class="open_all" v-if="is_all" @click="openAll">展开</a></p>
			</div>
			<div class="detai_content">
				<h3 class="detail_h">影人</h3>

				<swiper :options="swiperOption" class='swiper-top'>
			        <swiper-slide  v-for="cast in detail.casts" :key='1'>
			        	<router-link :to="{name:'celebrity',params:{id:cast.id}}">
			        		<img :src="cast.avatars.small">
			        		<p>{{cast.name}}</p>
			        	</router-link>
			        </swiper-slide>
			        <!-- <div class="swiper-pagination" slot="pagination"></div> -->
			     </swiper>

			</div>

			<!-- <common-tab :tabs='tabcontent' id='scroll_tab'></common-tab> -->
			<div id="scroll_tab" class="tab_box">
				<ul>
			  		<li :class="{active:is_comment}" @click="is_comment=true">短评论</li>
			  		<li :class="{active:!is_comment}" @click="is_comment=false">长影评</li>
			  	</ul>
			</div>
			<div id='tab_con' class="clearfix"></div>
			<div v-show='is_comment'>
				<comment-item :comments="comments.comments"></comment-item>
				<router-link :to="{name:'comments',params:{id:this.$route.params.id}}" class="more_comment" href="javascript:void(0)">全部短评{{comments.total}}条</router-link>
			</div>
			<div v-show='!is_comment'>
				<discuss-item :items="discuss.reviews"></discuss-item>
				<router-link :to="{name:'discuss',params:{id:this.$route.params.id}}" class="more_comment" href="javascript:void(0)">全部影评{{discuss.total}}条</router-link>
			</div>
		</div>


	</div>

</template>
<script>
	import Vue from 'vue'
	import VueAwesomeSwiper from 'vue-awesome-swiper'
	Vue.use(VueAwesomeSwiper)
	require('../assets/style/swiper-3.4.2.min.css')
	import Api from '../assets/js/api'
	import detailHeader from '../components/detail_header'
	import commonTab from '../components/half-tab'
	import commentItem from '../components/comment_item'
	import discussItem from '../components/discuss_item'
	import { swiper, swiperSlide } from 'vue-awesome-swiper'
	export default{
		name:'detail',
		components:{
			detailHeader,
			commonTab,
			swiper,
			swiperSlide,
			commentItem,
			discussItem
		},
		data(){
			return {
				detail:[],
				summary:'',
				comments:[],
				discuss:[],
				is_all:true,
				is_nav:true,
				is_comment:true,
		      	swiperOption: {
		          pagination: '.swiper-pagination',
		          slidesPerView: 4,
		          paginationClickable: true,
		          spaceBetween: 10,
		          freeMode: true
		        }
			}
		},
		mounted(){

			this.$nextTick(function () {
		        window.addEventListener('scroll', this.needToTop);
		        this.getDeatail();
				this.getDiscuss();
				this.getComment();
		      });
		},
		methods:{
			getDeatail(){
				var self=this;
				var thisId=this.$route.params.id;

        this.$http.jsonp(Api.url+'/v2/movie/subject/'+thisId).then(function(response){
          self.detail=response.body;
          self.cutSummary();
        });
			},
			getDiscuss(){
				var self=this;
				var movieId=this.$route.params.id;
        this.$http.jsonp(Api.url+'/v2/movie/subject/'+movieId+'/reviews?apikey=0b2bdeda43b5688921839c8ecb20399b&start=0&count=5').then(function(response){
          self.discuss=response.body;
        });
			},
			getComment(){
				var self=this;
				var movieId=this.$route.params.id;
        this.$http.jsonp(Api.url+'/v2/movie/subject/'+movieId+'/comments?apikey=0b2bdeda43b5688921839c8ecb20399b&start=0&count=5').then(function(response){
          self.comments=response.body;
          self.comments.is_zan=false
        });
			},
			cutSummary(){
				this.summary=(this.detail.summary).substr(0,56)+'...';
			},
			onStar(value){
    		return parseInt(value/10);
	    	},
	    	offStar(value){
	    		return 5-parseInt(value/10);
	    	},
	    	openAll(){
	    		this.summary=this.detail.summary;
	    		this.is_all=false;
	    	},
	    	needToTop(){
	    		var curHeight = document.documentElement.scrollTop || document.body.scrollTop;
	    		var scrollBar=document.getElementById('scroll_tab')
	    		let barTop=document.getElementById('tab_con').offsetTop;
	    		if(curHeight-barTop>=-50){
	    			scrollBar.style.position='fixed';
	    			scrollBar.style.top='0';
	    			this.is_nav=false;
	    		}else{
	    			scrollBar.style.position='static';
	    			this.is_nav=true;
	    		}
	    	}
		}
	}
</script>
<style>
  .loading{
    text-align: center;
    line-height:4;
    color: #888;
  }
	.tab_box{
		width: 100%;
	}
	.tab_box ul{
	/*position: fixed;*/
		width: 100%;
		height: 50px;
		line-height: 50px;
		border-bottom: 1px solid #f1f1f1;
		background: #fff;
		z-index: 2;
	}
	.tab_box ul li{
		float: left;
		width: 50%;
		text-align: center;
		color: #888;
	}
	.tab_box ul li.active{
		color: #474747;
		border-bottom: 2px solid #666;
	}
	.swiper-top{
		padding-top: 20px;
	}
	.swiper-slide{
		font-size: 12px;
		line-height: 2;
		text-align: center;
		color: #888;
	}
	.detail_pic{
		width: 100%;
		text-align: center;
		background: #4f4f4f;
	}
	.detail_pic img{
		margin:10px auto 30px;
		width: 160px;
	}
	.detail_top{
		overflow: hidden;
		padding: 16px ;
		border-bottom: 1px solid #f1f1f1;
	}
	.detail_title{
		margin-right: 94px;
		font-size: 18px;
		color: #333;
	}
	.detail_txt{
		margin-top: 8px;
		font-size: 12px;
		color: #aaa;
	}
	.star{
		font-size: 10px;
		color: #ccc;
	}
	.star .on{
		color: #feb10c;
	}
	.detail_grade{
		float: right;
		padding: 4px;
		width: 86px;
		height: 86px;
		text-align: center;
		font-size: 12px;
		color: #aaa;
		box-shadow: 2px 2px 5px rgba(0,0,0,.2)
	}
	.detail_grade .grade_num{
		font-size: 16px;
		color: #474747;
	}
	.detai_content{
		padding: 20px 16px;
	}
	.detail_h{
		font-size: 13px;
		color: #888;
	}
	.detail_desc{
		margin-top: 10px;
		font-size: 14px;
		color: #666;
	}
	.open_all{
		color: #15ef0a
	}
</style>
