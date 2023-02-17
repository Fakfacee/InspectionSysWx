<template>
	<view class="container">
		<view class="title-box">
            <view class="text_title">欢迎使用</view>
		    <view class="text_title">报检信息系统</view>
		</view>
		<view class="login-box">
			<view class="input-box">
				<image class="nameImage" src="../image/name.png"></image>
				<label class="loginLab">账号</label>
				<input class="inputText" placeholder="请输入手机号" v-model="phonenumber" /> 
			</view>
			<view class="whitedivide"></view>
			<view class="input-box">
				<image class="keyImage" src="../image/key.png"></image>
                <label class="loginLab">密码</label> 
                <input class="inputText" password="true" placeholder="请输入密码" v-model ="password" />
			</view>
		</view>
		
		<!--按钮--> 
		<view class="button-box">
			<button class = "buttonMain" @click="regisFun">注册</button>
			<button class = "buttonMain" @click="loginFun">登录</button> 
		</view> 
	</view>
</template>

<script>
	export default {
		data() {
			return {
				phonenumber : [],
				password : [],
					
			}
		},
		onLoad() {

		},
		methods: {
		//登录函数
		loginFun(e){
			if(this.phonenumber.length ==0 || this.password.length == 0){ 
			    uni.showToast({   
			        title: '用户名和密码不能为空',   
			        icon: 'none',   
			        duration: 2000   
			    })   
			}else{
				uni.request({
					url: getApp().globalData.url+'login',
					method : 'POST',
					dataType : 'JSON',
					
					data:{
						strUser : this.phonenumber,
						strPwd : this.password
					},
					success: (res) => {
					    var result = JSON.parse(res.data);
					    if(result.Status =='0'){
					    uni.showToast({
					
					      title: '用户名不存在,请进行注册',   
					      icon: 'loading',   
					      duration: 2000   
					      })   
					    }else if(result.Status =='1'){
							//用户名
							getApp().globalData.userName = result.Name,
							//承包商
							getApp().globalData.subcontractor = result.Contractor,
							//身份类别():0：管理员，1：车间管理人员，2：QC,3:焊工 class_code
							getApp().globalData.classCode = result.PowerId,
							//身份名:administrator,shopManage,QC,welder
							getApp().globalData.className,
							
							uni.switchTab({
								url:'/pages/main/main'
							    })
						}
					}
				
				
				})
			}
			
		},
		regisFun(){
			uni.navigateTo({
				url:'/pages/register/register'
			})
			
		}
	 
	}
}
</script>


<style>
.container{
	height: 100%;
	width: 100%;
	background-color: #FFFFFF;
	display: flex;
	flex-direction: column;
	
}

.title-box{
	display: flex;
	flex-direction: column;
	height: 30vh;
	
}

.login-box{
	padding-top: 5px;
	height: auto;
	display: flex;
	flex-direction: column;
	
}

.text_title{
  text-align: center;
  padding: 10px 10px;
  color: black; 
  font-size: 28px 
}
.input-box{
	height: 40px;
	display: flex;
	flex-direction: row;
	margin: 0 20px;
	background-color: #ededed;
}

.nameImage, .keyImage { 
  margin: 10px 10px; 
  width: 20px; 
  height: 20px 
} 
.loginLab { 
  margin: 10px 10px; 
  color: #545454; 
  font-size: 14px 
} 
.inputText { 
  flex: block; 
  float: right; 
  text-align: left; 
  margin: 10px 10px;
  color: black; 
  font-size: 14px } 

.button-box { 
  display: flex;
  flex-direction: column-reverse;
  width: 100%; 
  height: auto;
  margin-top: 10px; 
  margin-bottom: 20px; 
  padding-bottom: 0px;
   
} 

.buttonMain{
  width: 60%; 
  margin-top: 15px; 
  background-color: #ededed;
}
</style>
