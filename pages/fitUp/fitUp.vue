<template>
	<view class = "container">
		<view class="drawing">
			<view class="textMain">图纸号</view>
			<view class="textMain">{{drawingNo}}</view>
			<view class="graydivide"></view>
			<view class="blanke"></view>
			
			<view class="textMain">单管号</view>
			<view class="textMain">{{spoolNo}}</view>
			<view class="graydivide"></view>
			<view class="blanke"></view>
			<view class="textMain">选择当前焊口号</view>
			<radio-group @change="jointNoChange">
				<!--jointNoList类型为对象 item值,index键/索引-->
				<label class="uni-list-cell" v-for="(item,index) in jointNoList" :key="index">
					<view>
						<radio :value="item.value" :checked="index === current" />
					</view>
					<view>{{item.joint}}</view>
				</label>
			</radio-group>
			<view class="graydivide"></view>
			<view class="blanke"></view>
		</view>
		
		<view class="select-box">
			<view class="textMain">选择焊接工艺：</view>
			<radio-group @change="wpsChange">
				<label class="uni-list-cell" v-for="(item, index) in wpsList" :key="item.value">
					<view>
						<radio :value="item.value" :checked="index === current" />
					</view>
					<view>{{item.name}}</view>
				</label>
			</radio-group>
		</view>
		<view class="graydivide"></view>
		<view class = "welder-box">
			<view class="textMain">焊工号：</view>
			
			<view class="blanke"></view>
			<view class="textMain">{{welderNo}}</view>
		</view>
		<view class="graydivide"></view>
		<view class="weldeDate">
			<view class="textMain">焊接日期</view>
			
			<view class="blanke"></view>
			<view class="textMain">{{weldDate}}</view>
			
		</view>
		<view class="graydivide"></view>
		<view class="blanke"></view>
		<view class="select-box">
			<view class="textMain">选择当前地点：</view>
			<radio-group @change="locationChange">
				<label class="uni-list-cell" v-for="(item, index) in loacationList" :key="item.value">
					<view>
						<radio :value="item.value" :checked="index === current" />
					</view>
					<view>{{item.name}}</view>
				</label>
			</radio-group>
		</view>
		<!--
		<view class="location-box">
			<button class="buttonMain">获取当前位置</button>
			<view class="textMain">{{latitude}}</view>
			<view class="textMain">{{longitude}}</view>
			
		</view>
		-->
		<view class="button-box">
			<button class="buttonMain">提交</button>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
			drawingNo : '请求数据失败请刷新重试',
			spoolNo : '',
			jointNoList : [
			      {value: '1', joint: 'FW-1',checked: 'true'},
			      {value: '2', joint: '2'},
			      {value: '3', joint: '3'}
			    ],
			welderNo : 'CFHI0001',
			weldDate : '2023/2/8',
			
			latitude: 23.099994,
			longitude: 113.324520,
			wpsList: [
			      {value: '1', name: 'CS-101',checked: 'true'},
			      {value: '2', name: 'CS-301'},
			      {value: '3', name: 'CS-102'}
			    ],
			loacationList: [
			      {value: '1', name: '配套车间A跨',checked: 'true'},
			      {value: '2', name: '配套车间B跨'},
			      {value: '3', name: '其他地点(待添加)'}
			    ]
				
			}
		},
		methods: {
			
		jointNoChange: function(evt) {
		            for (let i = 0; i < this.items.length; i++) {
		                if (this.items[i].value === evt.detail.value) {
		                    this.current = i;
		                    break;
		                }
		            }
		        },
		wpsChange: function(evt) {
		            for (let i = 0; i < this.items.length; i++) {
		                if (this.items[i].value === evt.detail.value) {
		                    this.current = i;
		                    break;
		                }
		            }
		        },
		locationChange: function(evt) {
		            for (let i = 0; i < this.items.length; i++) {
		                if (this.items[i].value === evt.detail.value) {
		                    this.current = i;
		                    break;
		                }
		            }
		        }
		
			
			
		},
		onLoad() {
	
			uni.request({
				url:getApp().globalData.url + 'searchallweldbypipe',
				method : 'POST',
				dataType : 'JSON',
				data:{value :'0',spool:getApp().globalData.spool},
				success:(res) =>{
					    
				        var result = JSON.parse(res.data)
						//console.log(result)	0: {WeldId: 1800, WeldNo: "1", DrawingNo: "2-DO-35663-A0CA3Z_SHT1", JointType: "BW", Schedule: "S80", …}
                                              //1: {WeldId: 1804, WeldNo: "6", DrawingNo: "2-DO-35663-A0CA3Z_SHT1", JointType: "BW"					
				        var drawing = []
				        var lists = []
						//未考虑同单管不同图纸号情形--待完善
						drawing = result[0].DrawingNo
				        //for 循环,构造jointNoList结构类型数据
				        //console.log(Object.keys(result).length) 数组大小
				        for(let i = 0;i<Object.keys(result).length;i++)
				        {
							var object = new Object()
				            object.value = i
				            object.joint = result[i].WeldNo
							//console.log(object) {value: 1, joint: "6"}
						
							if(i ==0){
								//默认勾选第一栏
							    lists.push({ value: i, joint: result[i].WeldNo , checked: 'true' })
							
				            }else{
								
							    lists.push({ value: i, joint: result[i].WeldNo })
							}
							
				        }   
						    this.jointNoList = lists
						    this.drawingNo = drawing   
						    this.spoolNo = getApp().globalData.spool
				}
			})
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
	}
.buttonMain{
  width: 60%; 
  margin-top: 15px; 
  background-color: #ededed;
}

</style>
