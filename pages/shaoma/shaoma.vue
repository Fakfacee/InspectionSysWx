<template>
	<view class="container">
		<view class="text">单管号:</view>
		<view class="graydivide"></view>
	    <input class="inputText" placeholder="扫码或手动输入单管号" v-model="spool"></input>
		<view class="blanke-box"></view>

		<view class = "button-box">
		    <button class="buttonMain" @click="scanCodeEvent">扫码</button>
			
		    <button class="buttonMain" @click="submit">提交</button>
		</view>
	</view>	
	
</template>

<script>
	export default {
		data() {
			return {
				spool: [],
				activityType:[],
			}
		},
	
		methods: {
		
			
			get_text: function(e){
			    this.activityType = e.data.activityType
			  },
			scanCodeEvent: function(e){
				//h5端无法调用,小程序端调用需先配置APPID
				uni.scanCode({
					success:(res) => {
						//console.log('条码类型：' + res.scanType);QR_CODE
						//console.log('条码内容：' + res.result);2-DO-35663-A0CA3Z-01
						this.spool = res.result;

					}
				})
			},
			submit:function(e){
				uni.request({
					url:getApp().globalData.url+'searchaspool',
					method:"POST",
					dataType:"JSON",
					data:{value :'0',spool:this.spool},
					success:(res) =>{
						var result = JSON.parse(res.data)
						
						//console.log(result.Status)
					//1访问成功，0访问失败
					if (result.Status =='0') {
					
						uni.showToast({   
						          title: '无法查询到此单管，请检查后重试',   
						          icon: 'none',   
						          duration: 2000   
						      }) 
				
					}else if(result.Status =='1'){
						getApp().globalData.spool = this.spool;
 	
					    if(this.activityType == 'inspectFitUp'){
					        uni.navigateTo({
								url:'/pages/inspectFitUp/inspectFitUp'
					         })
					      }else if(this.activityType == 'inspectVisual'){
					        uni.navigateTo({
					
					          url: '/pages/inspectVisual/inspectVisual' 
					      
					          })
					      }else if(this.activityType == 'fitUp'){
					        uni.navigateTo({
					
					          url: '/pages/fitUp/fitUp'
					      
					          })
					      }else if(this.activityType == 'weld'){
					        uni.navigateTo({
					
					          url: '/pages/weld/weld'
					      
					          })
					      }
						
						
					}
					
						
					}
					
				})
				
				
			},
			
		},
		onLoad() {
	    this.activityType = getApp().globalData.activityType
			
		}
	}
</script>

<style>
.text{
	margin-top: 8px;
	margin-left: 6px;
    font-size: 20px;
}

.button-box{
	width: 100%;
	height: 40%;
	display: flex;
	flex-direction: column;
	align-items: center;
}
.blanke-box{
   height: 80px;

}
	
.buttonMain{
  width: 40%;
  margin-top: 15px; 
  background-color: #ededed;
}

.inputText {
  border: 2px solid #ededed;
  width: 60%;
  height: 40px;
  margin-left: 20%;
  text-align: center; 
  margin-top: 40px;
  color: black; 
  font-size: 14px 
  
  } 


</style>
