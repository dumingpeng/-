<template>
	<div class="indent">
		<div class="header">
			<p><i class="fa fa-chevron-left" @click="goback"></i>全部订单</p>
		</div>
		<div class="shop-cont " v-if="allIndent.length > 0">
			<ul>
				<li v-for="(message ,index) in allIndent" :index="index" >
					<img :src="'http://localhost:2000/uploads/'+ message.indentImage.split(',')[0]"/>
					<div class="">
						<p class="describe">{{ message.indentName }}&nbsp;&nbsp;&nbsp;{{ message.describe }}</p>
						<p class="price"><span class="prices">¥{{message.salePrice}}</span> <span class="affirm" @click="affirm(index)">×{{ message.indentNum }}</span></p>
					</div>
				</li>
			</ul>
	  </div>
	<div v-else>
		<p>没有商品哦</p>
	</div>
	<div class="footer">
	   <p><span @click="deleAll">清空订单</span></p>    	
	</div>
	</div>
</template>

<script>
	import axios from 'axios'
	export default{
		data:function(){
			return{
				allIndent:''
			}
		},
		mounted(){
			this.orderindent();
		},
		methods:{
			goback(){
    	    this.$router.go(-1)
            },
            orderindent(){
            	axios.post('/shop/indent/orderindent').then( (resData)=>{
            		if(resData.data.error == 0){
            			this.allIndent = resData.data.datas
            		}
            	}).catch( (error)=>{
            		alert(error);
            	})
            },
            deleAll(){
            	axios.post('/shop/indent/deleAllIndent').then( (resData)=>{
            		if(resData.data.error == 0){
            			this.allIndent = '';
            			
            		}
            	}).catch( (error)=>{
            		alert(error);
            	})
            }
		}
	}
</script>

<style scoped>
	.indent{
		padding-bottom: 40px;
	}
	.header{
		height: 50px;
		border-bottom: solid 1px #ccc;
		line-height: 50px;
		text-align: center;
		padding: 0 20px;
	}
	.header i{
		float: left;
		line-height: 50px;
	}
	.shop-cont ul{
		padding: 0;
		margin: 0;
		
	}
	.shop-cont ul li{
		overflow: hidden;
		padding: 0 10px;
		border-bottom: solid 1px #eee;
	}
	.shop-cont ul li img{
		width: 102px;
		float: left;
		margin-right: 10px;
	}
	.shop-cont ul li div .describe{
		margin-bottom: 40px;
	}
	.shop-cont ul li div .price{
		color: #FF0000;
		overflow: hidden;
	}
	.shop-cont ul li div .price .prices{
		display: inline-block;
		margin-top: 20px;
	}
	.shop-cont ul li div .price .affirm{
		/*background: #FF0000;*/
		/*padding: 8px;*/
		color: #FF0000;
		float: right;
		line-height: 56px;
		/*border-radius: 5px;*/
	}
	.footer{
		height: 20px;
		line-height: 20px;
		position: fixed;
		bottom: 0;
		text-align: right;
		width: 98%;
		padding: 10px;
		border-top: solid 1px #eee;
		background: white;
	}
	.footer p span{
		background: #FF0000;
		padding: 15px 30px;
		color: white;
	}
</style>