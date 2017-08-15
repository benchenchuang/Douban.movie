<template>
  <div class="search_wrap">
      <div class="search_bar">
          <a class="cancel_search" href="javascript:void(0);">取消</a>
          <div class="search_item">
              <i class="iconfont icon-sousuo"></i>
              <input class="search" type="search" placeholder="电影/电视剧/影人">
          </div>
      </div>
      <div class="search_list">
        <h3 class="search_title">热门搜索</h3>
        <ul class="search_content">
          <li>心理罪</li>
          <li>战狼2</li>
          <li>绝世高手</li>
          <li>银河护卫队2</li>
          <li>三生三世</li>
          <li>侠盗联盟</li>
          <li>生死之墙</li>
        </ul>
      </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search_wrap{
  background: #fff;
}
.search_bar{
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 44px;
  border-bottom: 1px solid #f1f1f1;
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
  margin: 5px 50px 5px 10px;
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
.search_list{
  margin-top: 45px;
}
.search_title{
  width: 100%;
  height: 32px;
  line-height: 32px;
  padding:0 16px;
  color: #ccc;
  box-sizing: border-box;
  background: #f7f7f7;
}
.search_content{
  padding:0 16px;

}
.search_content li{
  font-size: 13px;
  color: #888;
  height: 44px;
  line-height: 44px;
  border-bottom: 1px solid #f1f1f1;
}

</style>
