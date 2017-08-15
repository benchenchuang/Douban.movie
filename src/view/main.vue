<template>
  <div class="movie_wrap">
  		<keep-alive><router-view></router-view></keep-alive>
		  <common-footer></common-footer>
  </div>
</template>

<script>
  import commonFooter from '../components/common-footer'
  export default {
    name: 'movie_wrap',
    data () {
      return {
      }
    },
    components:{
    	commonFooter
    }
  }
</script>
