<script>
	export default {
		globalData : {
			//用户信息全部变量
			//名字
			name:['登陆后显示个人信息'],
			//焊工为焊工号，其它人员为身份标识码
			userId:[''],
			//单位--subcontractor
			subcontractor: [''],
			email:[''],
			phoneNumber:[],
			passWord:[],
			//权限
			userClassCode: [],
			//当前检验类型,当类型为[],getApp().globalData.activityType[0] = f 输出为第一个字符 
			activityType :[],
			//单管号
			spool : ['2-DO-35663-A0CA3Z-01'],
			//上线测试
			//url : ['http://1.116.137.136:8080/'],
			//本地测试
			url : ['http://127.0.0.1:5000/'],
			
		},
		
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
.whitedivide {/*白色分割线*/
  height: 1px;
  background-color: #FFFFFF;
  width: 56px;
  position:relative;
  top: 0px;
}

.graydivide {/*灰色分割条*/
  height: 2px;
  background-color: #ededed;
  position:relative;
  top: 0px;
}
.blanke{
height: 10px;
display: flex;
background-color: #ffffff;
}
.container{
	width: 100%;
	height: 100%;
	background-color: #FFFFFF;
	
}
.buttonMain{
  width: 40%; 
  margin-top: 15px; 
  background-color: #ededed;
}
.textMain{
	margin-top: 8px;
	margin-left: 6px;
	font-size: 20px;
}

	/*每个页面公共css */
</style>
