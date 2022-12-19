<template>
	<view class="box" @click="closepop(id)" style="width: 100vw;height: 100vw;">
		<image class="pic" src="../../static/backg.jpg" style="justify-self: start;position: absolute;width: 100vw;height:200vw;z-index:-10;" ></image>
		<view style="display:block; margin: 0 auto; width: 70vw; hight:70vw;margin-top: 8vw;">
		
			<view class="box3">
				<view style="margin-top: 17rpx;text-align: center;line-height: 15vw;position: relative;top: 170px;left: 15px;">
						
					<view v-for="(data, key) in dat1" :key='key.id' style="font-size: 45rpx;line-height：10vw">
					{{data[0]}} {{data[1]}} </view>
					<view v-for="(data, key) in dat2" :key='key.id' style="font-size: 45rpx;line-height：10vw">
					{{data[0]}} {{data[1]}}</view>
					<view v-for="(data, key) in dat3" :key='key.id' style="font-size: 45rpx;line-height：10vw">
					{{data[0]}} {{data[1]}} </view>
					<view v-for="(data, key) in dat4" :key='key.id' style="font-size: 45rpx;line-height：10vw">
					{{data[0]}} {{data[1]}}</view>
					
				</view>
			</view>
		
			
			<view class="box4">
					<view v-for="(data, key) in dat5" :key='key.id' style="display: inline-table; font-size: 60rpx;line-height：10vw;font-weight: bold;position: relative;top: 190px;left: 120px;">
					{{data[0]}}
					 </view>
			</view>
			

			<view class="box5">
				<view class="xun" style="display: flex;justify-content: space-around;width: 70vw;margin-top: 40rpx;position: relative;top: 170px;left: 10px;">
					
						<view class="xun1">
						<uni-transition :show="autoshow" :ref="ani_id0">
							<image style="width: 23vw;height: 23vw;border-radius: 100rpx;" src="../../static/xun.jpg" mode="aspectFill" @click="popout(0)"></image>
					    </uni-transition>
						</view>
					    <view class="xun2">
						<uni-transition :show="autoshow" :ref="ani_id1">
							<image style="width: 23vw;height: 23vw;border-radius: 100rpx;" src="../../static/xun.jpg" mode="aspectFill" @click="popout(1)"></image>
					    </uni-transition>
						</view>
						<view class="xun3">
						<uni-transition :show="autoshow" :ref="ani_id2">
							<image style="width: 23vw;height: 23vw;border-radius: 100rpx;" src="../../static/xun.jpg" mode="aspectFill" @click="popout(2)"></image>
					    </uni-transition>
						</view>
				    
				</view>
			</view>
		</view>	
		
	<view class="share">
			<image style=" bottom:0; right:0;width:25vw;height: 25vw;position: relative;top: 180px; right: -248px;" src="../../static/pic.jpg"></image>
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
				ani_id2 : "popout2"
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
						_sf.xuhua()
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
						_sf['ani_id'+id] = "popout" + id
					})
				}
			},
			xuhua(){
				
				},
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
		width: 100%;
		height: 100%;
		/* backdrop-filter:saturate(150%) contrast(50%) blur(8px);
		-webkit-backdrop-filter:saturate(150%) contrast(50%) blur(80px); */
		/* background-color:rgba(0,0,0,0~1); */
		    background-color: rgb(255, 255, 255,0.1);
		    box-shadow: 0 25px 45px rgba(0,0,0,0.1);
		    backdrop-filter: blur(4px);
	  }
	  20% {
		/* transform-origin:0px 280px; */
		transform:translateY(-400rpx);
		/* transform: scale(1); */
		/* width: 100%;
		height: 100%;
		backdrop-filter:saturate(150%) contrast(50%) blur(80px);
		-webkit-backdrop-filter:saturate(150%) contrast(50%) blur(8px); */
		/* background-color:rgba(0,0,0,0~1); */
		    background-color: rgb(255, 255, 255,0.1);
		    box-shadow: 0 25px 45px rgba(0,0,0,0.1);
		    backdrop-filter: blur(4px);
		

	  }
	  100% {
	     transform: scale(1); 
		
		}
	}
	
	@keyframes xuhua0{
		0%{
			background-color: rgb(255, 255, 255,0.1);
			box-shadow: 0 25px 45px rgba(0,0,0,0.1);
			backdrop-filter: blur(4px);
		}
		50%{
			background-color: rgb(255, 255, 255,0.1);
			box-shadow: 0 25px 45px rgba(0,0,0,0.1);
			backdrop-filter: blur(4px);
		}
		75%{
			background-color: rgb(255, 255, 255,0.1);
			box-shadow: 0 25px 45px rgba(0,0,0,0.1);
			backdrop-filter: blur(4px);
		}
		100%{
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
	.box{
		animation-name: xuhua0;
		animation-delay:2s;
		-webkit-animation-delay:0s;
		animation-timing-function: ease-in-out; 
		animation-iteration-count: 1; 
		animation-duration: 4s; 
	}
	.pic{
		animation-name: xuhua0;
		animation-delay:2s;
		-webkit-animation-delay:0s;
		animation-timing-function: ease-in-out; 
		animation-iteration-count: 1; 
		animation-duration: 4s; 
	}
	
	/* .xun1{ 
			animation-name: xun1; 
			animation-delay:2s;
			-webkit-animation-delay:2s;
			animation-timing-function: ease-in-out; 
			animation-iteration-count: 1; 
			animation-duration: 8s; 
			
	}
	.xun2{
			animation-name: xun1; 
			animation-delay:2s;
			-webkit-animation-delay:2s;
			animation-timing-function: ease-in-out; 
			animation-iteration-count: 1; 
			animation-duration: 8s; 
			
	}
	.xun3{
			animation-name: xun1; 
			animation-delay:2s;
			-webkit-animation-delay:2s;
			animation-timing-function: ease-in-out; 
			animation-iteration-count: 1; 
			animation-duration: 8s; 
			
	}
	
	
	.xun1：active{
		    background-color: rgb(255, 255, 255,0.1);
		    box-shadow: 0 25px 45px rgba(0,0,0,0.1);
		    backdrop-filter: blur(4px);
		
	} */
	.share{
		position:fixed; 
		bottom:0; 
		right:0;
		width:25vw;
		height: 25vw;
		background-color: aqua;
		position: relative;
		top: 180px;
		right: -250px;
	}
	
</style>

