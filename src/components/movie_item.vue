<template>
	<div>
			<router-link :to="{name:'detail',params:{id:item.subject.id}}" class="movie_item" v-for='(item,index) in items' :key="item.subject.id"  v-if="item.subject">
        <div class="rank_rating">
          <div class="line"></div>
          <span class="text" :class="{one:index+start+1==1,two:index+start+1==2,three:index+start+1==3}">{{index+start+1}}</span>
        </div>
        <div class="rank_info clearfix">
          <div class="info_pic">
            <img :src="item.subject.images.small">
          </div>
          <div class="info_box">
            <h3 class="name">{{item.subject.title}}</h3>
            <div class="star">
              <i class="iconfont icon-star on" v-for='star in onStar(item.subject.rating.stars)'></i>
              <i class="iconfont icon-star"  v-for='star in offStar(item.subject.rating.stars)'></i>
              <span>{{item.subject.rating.average}}</span>
            </div>
            <p class="txt">导演：<span v-for="director in item.subject.directors"> {{director.name}} </span></p>
            <p class="txt">演员：<span v-for="cast in item.subject.casts"> {{cast.name}} </span></p>
          </div>
        </div>
      </router-link>

      <router-link :to="{name:'detail',params:{id:item.id}}" class="movie_item" v-for='(item,index) in items' :key="item.id" v-if="!item.subject">
        <div class="rank_rating">
          <div class="line"></div>
          <span class="text" :class="{one:index+start+1==1,two:index+start+1==2,three:index+start+1==3}">{{index+start+1}}</span>
        </div>
        <div class="rank_info clearfix">
          <div class="info_pic">
            <img :src="item.images.small">
          </div>
          <div class="info_box">
            <h3 class="name">{{item.title}}</h3>
            <div class="star">
              <i class="iconfont icon-star on" v-for='star in onStar(item.rating.stars)'></i>
              <i class="iconfont icon-star"  v-for='star in offStar(item.rating.stars)'></i>
              <span>{{item.rating.average}}</span>
            </div>
            <p class="txt">导演：<span v-for="director in item.directors"> {{director.name}} </span></p>
            <p class="txt">演员：<span v-for="cast in item.casts"> {{cast.name}} </span></p>
          </div>
        </div>
		  </router-link>
	</div>
</template>
<script>
	export default{
		props:['items','start'],
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
<style scoped>
	.movie_item{
    display: block;
		padding: 0 16px;
		margin:30px 0;
    overflow: hidden;
	}

	.rank_rating{
		position: relative;
	    margin: 30px auto;
	    text-align: center;
	    height: 10px;
	    width: 50%;
	}
	.rank_rating .line{
		position: relative;
	}
	.rank_rating .line:after{
		display: block;
	    position: absolute;
	    left: 0;
	    top: 4px;
	    border-bottom: 1px solid #ddd;
	    width: 200%;
	    content: "";
	    transform-origin: 0 0;
	    -webkit-transform-origin: 0 0;
	    transform: scale(.5);
	    -webkit-transform: scale(.5);
	}
	.rank_rating .text{
		padding: 0 10px;
	    display: inline-block;
	    background-color: #fff;
	    position: absolute;
	    left: 50%;
	    top: -8px;
	    -webkit-transform: translateX(-50%);
	    transform: translateX(-50%);
	    font-size: 18px;
	    color: #888;
	}
	.text.one{
		color: #d71d1d;
	}
  .text.two{
		color: #ee4e07;
	}
  .text.three{
		color: #eeaa07;
	}
	.rank_info{
		padding: 16px;
		border: 1px solid #eee;
		box-shadow: 1px 1px 3px rgba(0,0,0,.05)
	}
  .info_pic{
    float: left;
    width:80px;
  }
  .info_box{
    margin-left: 90px;
  }
  .info_box .name{
    font-size: 18px;
    color: #000;
  }
  .star{
    color: #ccc;
  }
  .star span{
    margin-left:3px;
    font-size: 13px;
  }
  .star .on{
    color: #feb10c;
  }
  .info_box .txt{
    margin-top: 5px;
    font-size: 12px;
    color: #888;
  }
</style>
