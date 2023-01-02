<template>
	<view class="box" @click="closepop(id)" style="width: 100vw;height: 100vh;">
		<image class="pic" src="../../static/backg.jpg"style="justify-self:start; position:absolute;width: 100vw;height: 100vh;z-index: -10;" ></image>
		<view style="display:block; margin: 0 auto;">
		
			<view class="box3" style="overflow: hidden;">
				<view style="text-align:center; position:relative; margin-top: 350rpx; line-height:16vw;">
						
					<view v-for="(data, key) in dat1" :key='key.id' style="font-size: 50rpx;line-height：16vw;">
					{{data[0]}} {{data[1]}} </view>
					<view v-for="(data, key) in dat2" :key='key.id' style="font-size: 50rpx;line-height：16vw;">
					{{data[0]}} {{data[1]}}</view>
					<view v-for="(data, key) in dat3" :key='key.id' style="font-size: 50rpx;line-height：16vw;">
					{{data[0]}} {{data[1]}} </view>
					<view v-for="(data, key) in dat4" :key='key.id' style="font-size: 50rpx;line-height：16vw;">
					{{data[0]}} {{data[1]}}</view>
					
				</view>
			</view>
		
			
			<view class="box4">
					<view v-for="(data, key) in dat5" :key='key.id' style="display: inline-table; font-size: 60rpx;font-weight: bold;position: relative;margin-top: 10rpx;margin-left: 390rpx;">
					{{data[0]}}
					 </view>
			</view>
			

			<view class="box5">	
				<view class="xun" style="display: flex;justify-content: space-around;width:70vw;position: relative;margin-top: 10rpx;margin-left: 120rpx;">
				<view v-show="xuhua">
					<view class="cover" ></view>
				</view>
				
					
						<view class="xun1" @tap="on" style="flex: 1;z-index:500" >
						<uni-transition :show="autoshow" :ref="ani_id0">
							<image style="width: 23vw;height: 23vw;border-radius: 100rpx;" src="../../static/xun.jpg" mode="aspectFill" @click="popout(0)"></image>
					    </uni-transition>
						</view>
							
						
					
					    <view class="xun2" @tap="on" style="flex: 1;z-index:500">
						<uni-transition :show="autoshow" :ref="ani_id1">
							<image style="width: 23vw;height: 23vw;border-radius: 100rpx;" src="../../static/xun.jpg" mode="aspectFill" @click="popout(1)"></image>
					    </uni-transition>
						</view>
				
						
				
						<view class="xun3"@tap="on" style="flex: 1;z-index:500">
						<uni-transition :show="autoshow" :ref="ani_id2">
							<image style="width: 23vw;height: 23vw;border-radius: 100rpx;" src="../../static/xun.jpg" mode="aspectFill" @click="popout(2)"></image>
					    </uni-transition>
						</view>
					
					</view>
				
			</view>
		</view>
		
	<view class="share" style="overflow: hidden;margin-left: 520rpx;">
			<image class="share1" src="../../static/pic.jpg" style="width:28vw;height: 28vw;position: relative;" ></image>
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
				dat1 : [['食堂消费:',"2300"]],
				dat2 : [['用水消费:',"1000"]],
				dat3 : [['游泳消费:',"1000"]],
				dat4 : [['天猫消费:',"100"]],
				dat5 : [["9100"]],
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

