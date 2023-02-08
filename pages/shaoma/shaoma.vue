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
				spool: "",
				activityType:[],
			}
		},
		methods: {
			get_text: function(e){
			    this.spool = e.data.activityType
			  },
			scanCodeEvent: function(e){
				uni.scanCode({
					success: function (res) {
						this.spool = res.result;
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
					}
				})
			},
			submit:function(e){
				uni.request({
					url:getApp().globalData.url,
					method:"POST",
					dataType:"JSON",
					data:{value :'0',spool:this.spool},
					success:(res) =>{
						var result = JSON.parse(res.data)
						console.log(result.Status)
						console.log(result)
					if (result.Status =='0') {
					
						uni.showToast({   
						          title: '无法查询到此单管，请检查后重试',   
						          icon: 'none',   
						          duration: 2000   
						      }) 
				
					}else if(result.Status =='1'){
 	
					    if(this.activityType == 'inspectFitUp'){
					        uni.navigateTo({
								url:'/pages/inspectFitUp/inspectFitUp?activityType = inspectFitUp',
					         });
					      }else if(this.activityType == 'inspectVisual'){
					        wx.navigateTo({
					
					          url: '/pages/inspectVisual/inspectVisual?activityType = inspectVisual' ,
					      
					          });
					      }else if(this.activityType == 'fitUp'){
					        wx.navigateTo({
					
					          url: '/pages/fitUp/fitUp?activityType = fitUp',
					      
					          });
					      }else if(this.activityType == 'weld'){
					        wx.navigateTo({
					
					          url: '/pages/weld/weld?activityType = weld',
					      
					          }); 
					      }
						
						
					}
					
						
					}
					
				})
				
				
			},
			
		},
		onLoad:function(option){
			this.activityType = option.activityType
			
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
