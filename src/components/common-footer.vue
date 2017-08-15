<template>
  <div class="footer_wrap">
      <div class="nav_box">
          <ul>
              <router-link tag='li' :to="{name:'MovieList'}" class="nav_item">
                  <i class="iconfont icon-dianyingziyuan"></i>
                  <p class="nav_name">热映</p>
              </router-link>
              <router-link tag='li' :to="{name:'ranks'}" class="nav_item">
                  <i class="iconfont icon-yanjing"></i>
                  <p class="nav_name">找片</p>
              </router-link>
              <router-link tag='li' :to="{name:'about'}" class="nav_item">
                  <i class="iconfont icon-wode"></i>
                  <p class="nav_name">我的</p>
              </router-link>
          </ul>
      </div>
  </div>
</template>

<script>
  export default {
    name: 'footer',
    data () {
      return {
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.footer_wrap{
  height: 44px;
}
.nav_box{
  width: 100%;
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
    box-shadow: -2px 0 4px rgba(0,0,0,.15);
  background: #fff;
  z-index: 2;
}
.nav_box .nav_item{
  float: left;
  padding:5px 0;
  width: 33.333%;
  line-height: 1.3;
  text-align: center;
  color:#aaa;
  box-sizing: border-box;
}
.nav_box .nav_item.router-link-active.router-link-exact-active{
  color: #222;
}
</style>
