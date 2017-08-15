<template>
	<div>
		<detail-header :title="title"></detail-header>
		<work-list :works='works' v-infinite-scroll="getWorks" infinite-scroll-distance="100"></work-list>
	</div>
</template>
<script>
	import Vue from 'vue';
	  //滚动
	import infiniteScroll from 'vue-infinite-scroll'
	Vue.use(infiniteScroll);
	import detailHeader from '../components/detail_header'
	import workList from '../components/work_list'
	import Api from '../assets/js/api'
	export default{
		components:{
			detailHeader,
			workList
		},
		data(){
			return{
				title:"全部作品",
				id:this.$route.params.id,
				getNum:10,
				works:[]
			}
		},
		mounted(){
			this.getWorks()
		},
		methods:{
			getWorks(){
				var self=this;
        this.$http.jsonp(Api.url+'/v2/movie/celebrity/'+self.id+'/works?apikey=0b2bdeda43b5688921839c8ecb20399b&start=0&count='+self.getNum).then(function(response){
          self.works=response.body.works;
          self.getNum+=10
        });
			}
		}
	}
</script>
