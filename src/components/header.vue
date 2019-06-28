<template>
	<header>
      <div class="headLeft">        
        <a href="/"><img src="../assets/images/logo.png"></a>
        <span>World Cities Weather <br>Cold or warm</span>
      </div>
      <div class="headRight" v-if="isVisible">
	      <div class="cityName">
	      	{{ cityName }} - {{ countryName }}
	      </div>
      </div>
    </header>	
</template>

<script>
	export default{
		props : {
			isVisible : {
				type : Boolean
			},
			cityName : {
				type : String
			},		
			countryName : {
				type : String
			}	
		}
	} 
</script>

<style lang="scss" scoped>
	header {display: flex; align-items: center; justify-content: space-between; padding:15px; margin:0 auto 20px; width:100%; background: #909ccf; z-index:2;
		.headLeft{display: flex; height:60px; align-items: center;}
		.headRight{display: flex; align-items: center;}
		a{padding-right: 15px; float:left;
			img{max-width: 60px}
		}
		span{font-size:22px; line-height: 28px; float:left; color:#fff;}
		.cityName{float:left; width:auto; text-align: center; font-size:16px; border-radius: 0px; color:#fff; background:rgba(103, 126, 210, 0.6); padding:10px 20px; margin:0 10px;}
		.newSearch{color:#fff;}
	}
	@media (max-width: 1023px) {
		header {flex-direction: column;}
		header span{font-size:16px; line-height: 20px;}
		header .headRight{margin-top: 10px;}
	}
</style>