<template>
	<div>
		<router-link class='search_item_box' tag='div' :to="{name:'detail',params:{id:subject.id}}" v-for='subject in searchs' :key='subject.id'>
          <img :src="subject.images.small">
          <div class="item_info">
            <h3>{{subject.title}}</h3>
            <p>{{subject.rating.average}}分 / {{subject.year}}</p>
          </div>
        </router-link>
	</div>
</template>
<script>
	export default{
		props:['searchs']
	}
</script>
<style scoped>
	.search_item_box{
		width: 100%;
		padding: 20px;
		border-bottom: 1px solid #f1f1f1;
		box-sizing: border-box;
		overflow: hidden;
	}
	.search_item_box img{
		float: left;
		width:60px;
		overflow: hidden;
	}
	.item_info{
		margin-left: 80px;
		color: #888;
		font-size: 12px;
		line-height: 2;
	}
	.item_info h3{
		font-size: 16px;
		color: #474747;
	}
</style>