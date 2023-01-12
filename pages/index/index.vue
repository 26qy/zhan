<template>
	<view class="box" @click="closepop(id)" style="width: 100vw;height: 100vh;">
		<image class="pic" src="../../static/分享界面（1）.jpg"style="justify-self:start; position:absolute;width: 100vw;height: 100vh;z-index: -10;" ></image>
		<view style="display:block; margin: 0 auto;">
		
			<view class="box3" style="overflow: hidden;">
				<view style="text-align:center; position:relative; margin-top: 280rpx; line-height:16vw;">
						
					<view v-for="(data, key) in dat1" :key='key.id' style="font-size: 40rpx;line-height：16vw;margin-left: 10rpx;">
					{{data[0]}} {{data[1]}} </view>
					<view v-for="(data, key) in dat2" :key='key.id' style="font-size: 40rpx;line-height：16vw;margin-left: 10rpx;">
					{{data[0]}} {{data[1]}}</view>
					<view v-for="(data, key) in dat3" :key='key.id' style="font-size: 40rpx;line-height：16vw;margin-left: 10rpx;">
					{{data[0]}} {{data[1]}} </view>
					<view v-for="(data, key) in dat4" :key='key.id' style="font-size: 40rpx;line-height：16vw;margin-left: 10rpx;">
					{{data[0]}} {{data[1]}}</view>
					
				</view>
			</view>
		
			
			<view class="box4">
					<view v-for="(data, key) in dat5" :key='key.id' style="display: inline-table; font-size: 50rpx;font-weight: bold;position: relative;margin-top: 10rpx;margin-left: 250rpx;">
					{{data[0]}}
					 </view>
			</view>
			

			<view class="box5">	
				<view class="xun" style="display: flex;justify-content: space-around;width:58vw;position: relative;margin-top: 10rpx;margin-left: 120rpx;">
				<view v-show="xuhua">
					<view class="cover" ></view>
				</view>
				
					
						<view class="xun1" @tap="on" style="flex: 1;z-index:500" >
						<uni-transition :show="autoshow" :ref="ani_id0">
							<image style="width: 20vw;height: 20vw;border-radius: 100rpx;" :src="msg1>2500?url1:url2" mode="aspectFill" @click="popout(0)"></image>
					    </uni-transition>
						</view>
							
						
					
					    <view class="xun2" @tap="on" style="flex: 1;z-index:500">
						<uni-transition :show="autoshow" :ref="ani_id1">
							<image style="width: 20vw;height: 20vw;border-radius: 100rpx;" :src="msg2<1200?url3:url4" mode="aspectFill" @click="popout(1)"></image>
					    </uni-transition>
						</view>
				
						
				
						<view class="xun3"@tap="on" style="flex: 1;z-index:500">
						<uni-transition :show="autoshow" :ref="ani_id2">
							<image style="width: 20vw;height: 20vw;border-radius: 100rpx;" :src="msg3>700?url5:url6" mode="aspectFill" @click="popout(2)"></image>
					    </uni-transition>
						</view>
					
					</view>
				
			</view>
		</view>
		
	<view class="share" style="overflow: hidden;margin-left: 480rpx;margin-top: 110rpx;">
			<image class="share1" src="../../static/pic.jpg" style="width:22vw;height: 22vw;position: relative;" ></image>
		</view> 
	
	<view>
		<uni-transition ref="closepop"></uni-transition>
	</view>
		
	 </view>

</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				dat1 : [['食堂消费:',2300]],
				dat2 : [['用水消费:',1000]],
				dat3 : [['游泳消费:',400]],
				dat4 : [['天猫消费:',3200]],
				dat5 : [["9100"]],
				msg1 : "",
				msg2 : "",
				msg3 : "",
				url1:require("../../static/3.jpg"),
				url2:require("../../static/4.jpg"),
				url3:require("../../static/5.jpg"),
				url4:require("../../static/6.jpg"),
				url5:require("../../static/1.jpg"),
				url6:require("../../static/2.jpg"),
				show: false,
				autoshow : true,
				hadxun : 0,
				id:"",
				// ani_id : "popout",
				ani_id0 : "popout0",
				ani_id1 : "popout1",
				ani_id2 : "popout2",
				xuhua:false,
				cancle:false,
			}
		},
		onLoad() {
			
		},
		onReady(){
			
			this.$refs.popout0.init({
				duration : 200,
				timingFunction : "linear",
				delay : 0
			})
			this.$refs.popout1.init({
				duration : 200,
				timingFunction : "linear",
				delay : 0
			})
			this.$refs.popout2.init({
				duration : 200,
				timingFunction : "linear",
				delay : 0
			})
			this.$refs.closepop.init({
				duration : 200,
				timingFunction : "linear",
				delay : 0
			})
			// this.$refs.popout.init({
			// 	duration : 200,
			// 	timingFunction : "linear",
			// 	delay : 0
			// })
			
		},
		methods: {
			xun(){
				var msg1 = dat1[1];
				var msg2 = dat2[1];
				var msg3 = dat3[1];
			},
			
			popout(id) {
				if(!this.hadxun){
					var _sf = this;
					// this.$refs['popout'+id].step({
					// 	scale: [2, 2],
					// 	translateY : "-200rpx"
					// })
					this.$refs.popout0.step({
						scale: [2, 2],
						translateY : "-200rpx",
						translateX : "100rpx",
					})
					this.$refs.popout1.step({
						scale: [2, 2],
						translateY : "-200rpx"
					})
					this.$refs.popout2.step({
						scale: [2, 2],
						translateY : "-200rpx",
						translateX : "-100rpx",
						
					})
					this.$refs['popout'+id].run(()=>{
						// console.log('hhh')
						_sf.on()
						_sf.hadxun = id+1
						_sf['ani_id'+id] = "closepop" 
					})	
				}
			},
			closepop(){
				var _sf = this;
				if(this.hadxun){
					let id = this.hadxun - 1;
					this.$refs.closepop.step({
						translateY : "1rpx",
						translateX : "1rpx",
					 	scale: [1, 1]
					})
					this.$refs.closepop.run(()=>{
						// console.log('jjj')
						_sf.hadxun = 0
						_sf.off()
						_sf['ani_id'+id] = "popout" + id
					})
				}
			},
			on(){
				this.xuhua=true;
			},
			logout(){
				this.xuhua=true;
			},
			off(){
				this.xuhua=false;
			}
			
			// show(){
			// 	this.$refs.popout.step({
			// 		translateY : "-200rpx",
			// 	 	scale: [1, 1]
			// 	})
			// 	this.$refs.popout.run(()=>{
			// 		// console.log('jjj')
			// 		_sf.hadxun = 0
			// 		_sf['ani_id'+id] = "popout" + id
			// 	})
			// }
			
			
			
		}

	}
</script>

<style>
	 @keyframes xun1{
	  
	  0% {
	   /* transform: scale(1); */
		transform:translateY(-400rpx);
	  }
	  10% {
	    transform:translateY(-400rpx);
	  }
	  80% {
		transform:translateY(-400rpx);
		 transform: scale(1.25);
	  }
	  100% {
	     transform: scale(1); 
		
		}
	}
	
	.xun{
			animation-name: xun1; 
			animation-delay:2s;
			-webkit-animation-delay:0s;
			animation-timing-function: ease-in-out; 
			animation-iteration-count: 1; 
			animation-duration: 4s; 
			
	}
	.cover{
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0,0,0,0.5);
		z-index: 200;
	}
	
	/* .share{
		position: relative;	
	}
	.share1{
		position: relative;	
		margin-left: 500rpx;
		
	} */
	
</style>

