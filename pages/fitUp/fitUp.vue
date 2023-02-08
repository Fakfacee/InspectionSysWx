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
				<label class="uni-list-cell" v-for="(item, index) in jointNoList" :key="item.value">
					<view>
						<radio :value="item.value" :checked="index === current" />
					</view>
					<view>{{item.name}}</view>
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
		<view class="location-box">
			<button class="buttonMain">获取当前位置</button>
			<view class="textMain">{{latitude}}</view>
			<view class="textMain">{{longitude}}</view>
			
		</view>
		
		<view class="button-box">
			<button class="buttonMain">提交</button>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
			drawingNo : '',
			spoolNo : '',
			jointNoList : [
			      {value: '1', name: 'FW-1',checked: 'true'},
			      {value: '2', name: '2'},
			      {value: '3', name: '3'}
			    ],
			welderNo : 'CFHI0001',
			weldDate : '2023/2/8',
			
			latitude: 23.099994,
			longitude: 113.324520,
			wpsList: [
			      {value: '1', name: 'CS-101',checked: 'true'},
			      {value: '2', name: 'CS-301'},
			      {value: '3', name: 'CS-102'}
			    ]
				
			}
		},
		methods: {
			
		radioChange: function(evt) {
		            for (let i = 0; i < this.items.length; i++) {
		                if (this.items[i].value === evt.detail.value) {
		                    this.current = i;
		                    break;
		                }
		            }
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
	}
.buttonMain{
  width: 60%; 
  margin-top: 15px; 
  background-color: #ededed;
}

</style>
