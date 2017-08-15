<template>
	<div>
    <div>
      <detail-header :title="content.name"></detail-header>

      <div class="detail_pic">
        <img :src="content.avatars.medium">
      </div>
      <div class="celebrity_box">

        <div class="cele_top">
          <h2>{{content.name}}</h2>
          <p>{{content.name_en}}</p>
        </div>
        <div class="cele_desc">
          <div class="celebrity_info">
            <p><span class="label">性别：</span>{{content.gender}}</p>
            <p><span class="label">出生地：</span>{{content.born_place}}</p>
            <p><span class="label">英文名：</span><span v-for="aka in content.aka_en"> {{aka}} </span></p>
          </div>
        </div>
        <h3 class="cele_title">代表作品</h3>
        <swiper :options="swiperOption" class='swiper-top'>
          <swiper-slide  v-for="item in content.works" :key='1'>
            <router-link :to="{name:'detail',params:{id:item.subject.id}}">
              <img :src="item.subject.images.small">
              <p>{{item.subject.title}}</p>
              <div class="star">
                <i class="iconfont icon-star on" v-for='star in onStar(item.subject.rating.stars)'></i>
                <i class="iconfont icon-star"  v-for='star in offStar(item.subject.rating.stars)'></i>
              </div>
            </router-link>
          </swiper-slide>
          <!-- <div class="swiper-pagination" slot="pagination"></div> -->
        </swiper>
        <router-link class='more_works' :to="{name:'moreworks',params:{id:this.$route.params.id}}">全部作品<i class="iconfont icon-right"></i></router-link>
      </div>


    </div>

  </div>
</template>
<script>
	import Vue from 'vue'
	import VueAwesomeSwiper from 'vue-awesome-swiper'
	Vue.use(VueAwesomeSwiper);
	import { swiper, swiperSlide } from 'vue-awesome-swiper'

	import Api from '../assets/js/api'
	import detailHeader from '../components/detail_header'
	export default{
		components:{
			detailHeader,
			swiper,
			swiperSlide
		},
		data(){
			return{
				id:this.$route.params.id,
				content:[],
				swiperOption: {
		          pagination: '.swiper-pagination',
		          slidesPerView: 3,
		          paginationClickable: true,
		          spaceBetween: 10,
		          freeMode: true
		        }
			}
		},
		mounted(){
			this.getCelebrity()
		},
		methods:{
			getCelebrity(){
				var self=this;
        this.$http.jsonp(Api.url+'/v2/movie/celebrity/'+self.id).then(function(response){
          self.content=response.body;
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
<style scoped>
	.more_works{
		display: block;
		width: 100%;
		height: 50px;
		line-height: 50px;
		font-size: 16px;
		color: #474747;
	}
	.more_works .iconfont{
		float: right;
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
	.celebrity_box{
		padding: 16px 16px 0;
	}
	.cele_top{
		color: #474747;
		font-size: 12px;
		line-height: 1.2;
	}
	.cele_top h2{
		font-size: 22px;
	}
	.cele_desc{
		margin-top: 20px;
		overflow: hidden;
	}
	.avatar{
		float: left;
	}
	.avatar img{
		width: 100px;
	}
	.celebrity_info{
		color: #888;
		line-height: 2;
	}
	.celebrity_info .label{
		display: inline-block;
		width: 60px;
	}
	.swiper-top p{
		margin-top: 5px;
		line-height: 1.5;
		height: 36px;
	}
	.cele_title{
		margin: 15px 0 10px;
		color: #888;
	}
	.star{
		font-size: 12px;
		color: #ddd;
	}
	.star .on{
		color: #feb10c
	}
</style>
