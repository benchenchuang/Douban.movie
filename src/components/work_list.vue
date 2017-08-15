<template>
	<div>
		<router-link tag="div" :to="{name:'detail',params:{id:work.subject.id}}" class="movie_item" v-for="work in works" :key="work.subject.id">
			<div class="pic">
				<img :src="work.subject.images.small">
			</div>
			<div class="movie_desc">
				<h3 class="title">{{work.subject.title}}</h3>
				<div  v-if='work.subject.rating.stars==0'>
					<p class="no_num">暂无评分</p>
				</div>
				<div class="star" v-else>
					<i class="iconfont icon-star on" v-for='star in onStar(work.subject.rating.stars)'></i>
					<i class="iconfont icon-star"  v-for='star in offStar(work.subject.rating.stars)'></i>
					<span>{{work.subject.rating.average}}</span>
				</div>
				<p class="txt" v-if="work.subject.directors.length">导演:<span v-for='doctor in work.subject.directors'> {{doctor.name}} </span> </p>
				<p class="txt" v-if="work.subject.casts.length>0">主演:<span v-for="cast in work.subject.casts"> {{cast.name}} </span> </p>
				<div class="profess">
					<span class="scan" v-for="role in work.roles">{{role}}</span>
				</div>
			</div>
		</router-link>
	</div>
</template>
<script>
	export default{
		props:['works'],
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
<style>

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
}
.movie_desc p{
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
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
.no_num{
	font-size: 12px;
	color: #aaa;
	line-height: 2.4;
}
.profess{
	margin-top: 10px;
	font-size: 12px;
	color: #888;
	overflow: hidden;
}
.profess span{
	float: left;
	margin-right: 10px;
	padding: 2px 5px ;
	background: #f4f4f4;
}
</style>