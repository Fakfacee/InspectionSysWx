<template>
	<view class="container">
		<view class="text-box">
			<text>请填写以下信息以完成注册</text>
			<text>人员类别</text>
			<radio-group @change="classChange">
				<label class="uni-list-cell" v-for="(item, index) in className" :key="item.value">
					<view>
						<radio :value="item.value" :checked="index === current" />
					</view>
					<view>{{item.name}}</view>
				</label>
			</radio-group>
			<view class="graydivide"></view>
			<view class="blanke"></view>
			<text>所属公司</text>
			<input class="inputText" placeholder="CFHI" v-model="subcontractor"></input>
			<view class="blanke"></view>
			
			<text>焊工号或其他标识ID</text>
			<input class="inputText" placeholder="CFHI0001" v-model="identity"></input>
			<view class="blanke"></view>
			
			<text>手机号</text>
			<input class="inputText" v-model="phoneNumber"></input>
			<view class="blanke"></view>
			<text>密码</text>
			<input class="inputText" v-model="passWord"></input>
			<view class="button-box">
			    <button class="buttonMain" @click="submitFun">提交</button>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				className :[
			      {value: '1', name: '车间管理人员',checked: 'true'},
			      {value: '2', name: 'QC'},
			      {value: '3', name: '焊工'}
			    ],
				//current,当前位置 0第一位
				current : 0,
				//权限码默认0,0：车间管理人员，1：QC,2:焊工
				classCode : 1,
				subcontractor : [],
				phoneNumber : [],
				passWord : [],
				identity : [],
			}
		},
		methods: {
			classChange: function(evt) {
			            for (let i = 0; i < this.className.length; i++) {
			                if (this.className[i].value === evt.detail.value) {
			                    this.current = i;
								this.classCode = i+1
			                    break;
			                }
			            }
			        },
			
			submitFun(){
				uni.request({
					url:getApp().globalData.url + 'register',
					method:'POST',
					dataType:'JSON',
					data:{
						code:this.classCode,
						contractor:this.subcontractor,
						
						phoneno:this.phoneNumber,
						welder:this.identity,
						password:this.passWord
					},
					success:(res) =>{
						var result = JSON.parse(res.data)
						if(result.Status =='1'){
							uni.navigateTo({
							          //重新返回登录界面
							          url: '/pages/index/index',
									})
						}else if(result.Status =='0'){
							
							wx.showToast({   
							            title: '该手机号码已注册',   
							            icon: 'none',   
							            duration: 2000   
							          })   
							
						}	
					},
					fail:(res)=>{
					        wx.showToast({   
					          title: '请求失败，请重试或与管理员取得联系',   
					          icon: 'none',   
					          duration: 2000   
					        })  
					
					      }
				})
				
				
				
			}
			
		}
	}
</script>

<style>
.uni-list-cell {
	    height: 40px;
	    display: flex;
		margin-left: 8px;
		flex-direction: row;
	    align-items: center;
		font-size: 18px;
	},
.inputText { 
  flex: block; 
  text-align: left; 
  width: 60%;
  height: 30px;
  margin-top: 10px;
  margin-bottom: 10px;
  margin-left: 8px;
  color: black; 
  font-size: 14px;
  border-style: solid;
  border-width: 1px;
  border-color: #ededed;
  } 
	
	

</style>
