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
			
			//上线测试
			//url : ['http://1.116.137.136:8080/'],
			//本地测试
			url : ['http://127.0.0.1:8080/'],
			
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
  height: 10px;
  background-color: #ededed;
  position:relative;
  top: 0px;
}
.blanke{
height: 10px;
display: flex;
background-color: #ffffff;
}

	/*每个页面公共css */
</style>
