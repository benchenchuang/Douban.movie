<template>
  <div class="tab_box">
  	<ul>
  		<router-link tag='li' :to="{name:tab.name,params:{id:tab.id}}" v-for="tab in tabs" :key='tab.id'>{{tab.title}}</router-link>
  	</ul>
  </div>
</template>

<script>
  export default {
    name: 'half-tab',
    props:['tabs'],
    data () {
      return {
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.relocate ul{
  position: fixed;
}
.tab_box{
	width: 100%;
	height: 50px;
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
.tab_box ul li.router-link-exact-active.router-link-exact-active{
	color: #474747;
	border-bottom: 2px solid #666;
}
</style>
