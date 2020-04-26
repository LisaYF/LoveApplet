<template>
	<view class="content">
		<image src="../../static/g1.gif" mode="widthFix"></image>
		<text class="title">小姐姐，做我女朋友吧</text>
		<view class="operate">
			<button type="primary" class="btn" @tap="agree">好呀</button>
			<button type="warn" class="btn" @tap="disagree">不好</button>
		</view>
		<view class="message" v-for="one in love" :key="one">{{one}}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				love:[],
				timer:{}
			}
		},
		onLoad() {
			this.back=uni.getBackgroundAudioManager()
			this.back.src="http://140.143.132.225/love/pdd.mp3"
			this.back.title="音乐"
			this.back.play()
		},
		onShow() {
			this.love=[]
			this.timer={}
			let msg={
				2000:"小姐姐，我爱你！",
				4000:"xiaojiejie, I love you! (英语)",
				6000:"お姉さん、愛してる! (日语)",
				8000:"Kleine schwester, ich liebe dich! (德语)",
				10000:"Сестрёнка, я люблю тебя! (俄语)",
				12000:"Piccola sorella, ti amo! (意大利语)",
				14000:"¡Pequeña hermana, te amo! (西班牙语)",
				16000:"작은 누나, 사랑해요! (韩语)",
				18000:"Em gái, anh yêu em! (越南语)",
				20000:"Irmã, eu amo-te! (葡萄牙语)"
			}
			let ref=this;
			for (let key in msg){
				let t=setTimeout(function(){
					ref.love.push(msg[key])
					delete ref.timer[key]
				},key)
				ref.timer[key]=t
			}
		},
		onHide:function(){
			for(let key in this.timer){
				clearTimeout(this.timer[key])
			}
		},
		methods: {
			agree:function(){
				uni.showToast({
					icon:"none",
					title:"小姐姐，晚上下班一起走吧！",
					duration:4000
				})
			},
			disagree:function(){
				uni.showModal({
					title:"小姐姐，要不要再想想？",
					content:"拒绝了，可就没有大红包了：）",
					cancelText:"拒绝",
					confirmText:"同意",
					success:function(res){
						if(res.confirm){
							uni.showToast({
								icon:"none",
								title:"我就知道小姐姐一定会同意的：）",
								duration:4000
							})
						}
						else{
							uni.showToast({
								icon:"none",
								title:"真遗憾，你错过了一个亿的大红包",
								duration:4000
							})
						}
					}
				})
			}
		}
	}
</script>

<style lang="less">
	@import url("index.less");
</style>
