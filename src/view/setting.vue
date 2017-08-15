<template>
	<div>
		<detail-header :title="title"></detail-header>
		
		<div class="setting_box">
			<ul>
				<li>意见反馈<span class="fr"><i class="iconfont icon-right"></i></span></li>
				<li>给应用评分<span class="fr"><i class="iconfont icon-right"></i></span></li>
				<li>清除缓存<span class="fr" @click="clear">{{contain}}<i class="iconfont icon-right"></i></span></li>
				<li>关于<span class="fr"><i class="iconfont icon-right"></i></span></li>
			</ul>
		</div>

	</div>
</template>
<script>
	import detailHeader from  '../components/detail_header'
	export default{
		components:{
			detailHeader
		},
		data(){
			return{
				title:'我的设置',
				contain:'5.2Mb'
			}
		},
		methods:{
			clear(){
				
				setTimeout(()=>{
					alert('清除完毕！')
					this.contain=''
				},500)
			}
		}
	}
</script>
<style scoped>
	.setting_box{
		border-top:1px solid #f1f1f1;
		border-bottom:1px solid #f1f1f1;
		padding: 0 16px;
	}
	.setting_box li{
		height: 50px;
		line-height: 50px;
		color: #474747;
		border-bottom: 1px solid #f1f1f1;
		overflow: hidden;
	}
	.setting_box li:last-child{
		border-bottom: none;
	}
	.setting_box li .fr{
		float: right;
		color: #aaa;
		font-size: 12px;
	}
</style>