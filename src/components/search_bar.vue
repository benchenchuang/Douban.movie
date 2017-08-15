<template>
	  <router-link tag='div' class="search_tab" :to="{name:'search'}">
       <div class="search_bar">
        <div class="search_item">
            <i class="iconfont icon-sousuo"></i>
            <input class="search" type="search" placeholder="电影/电视剧/影人">
        </div>
      </div> 
    </router-link>
</template>
<script>
	export default{

	}
</script>
<style>
.search_tab{
  width: 100%;
  height: 44px;
}
.search_bar{
  position: fixed;
  left: 0;
  top:0;
  width: 100%;
  height: 44px;
  background: #fff;
  border-bottom: 1px solid #f1f1f1;
  z-index: 10;
}
.cancel_search{
  float: right;
  width: 48px;
  text-align: center;
  font-size: 14px;
  color: #15ef0a;
  height: 44px;
  line-height: 44px;
}
.search_item{
  position: relative;
  margin: 5px 10px;
  height: 34px;
  line-height: 34px;
  background: #eaeaea;
  border-radius: 6px;
  overflow: hidden;
}
.search_item .iconfont{
  float: left;
  width: 20px;
  color: #aaa;
  padding: 0 10px;
}
.search_item .search{
  position: absolute;
  width: 100%;
  left: 40px;
  top: 0;
  right: 0;
  height: 34px;
  line-height: 34px;
}
</style>