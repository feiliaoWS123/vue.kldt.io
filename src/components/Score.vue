<template>
	<div >
		<!--分数-->
		<div class="my_score_container">
			<p class="my_score">
				<span class="fenshu">{{score}}</span>
				<span class="fenshu">分!</span>
			</p>
			<p class="pingjia">{{tips}}</p>
		</div>
		<!--分享按钮-->
		<div class="share" @click="isShow = true"></div>
		<!--遮罩层-->
		<div class="mask" v-show="isShow" @click="isShow = false">
			<img src="../assets/5-2.png" class="share_img" />
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return {
				//我选择的答案
				myAnsers:this.$store.state.myAnsers,
				//正确答案
				rightAnswers:this.$store.state.rightAnswers,
				//分享
				isShow:false,
				//分数
				score:0,
				//鼓励的话
				tips:""
			}
		},
		created:function(){
			var that = this;
			//计算分数
			that.myAnsers.forEach(function(item,index){
				if (item == that.rightAnswers[index]) {
					that.score += 20;
				}
			});
			if (that.score == 0) {
				that.tips = "呀！一道题都没对"
			} else if(that.score == 20){
				that.tips = "加油！加油！"
			} else if(that.score == 40){
				that.tips = "再努力一点！"
			} else if(that.score == 60){
				that.tips = "恭喜及格！"
			} else if(that.score == 80){
				that.tips = "不错！不错！"
			} else if(that.score == 100){
				that.tips = "nice"
			}
		}
	}
</script>

<style lang="less">
	/*重写body演示,换一张背景图*/
	body{
		background: url(../assets/4-1.jpg) no-repeat;
		background-size: 100% 100%;
	}
	/*分数开始*/
	.my_score_container{
		background: url(../assets/4-2.png) no-repeat;
		background-size: 100% 100%;
	    width: 10rem;
	    height: 8rem;
	    position: absolute;
	    top: 6rem;
	    left: 50%;
	    margin-left: -5rem;
	    .my_score{
	    	    text-align: center;
			    position: absolute;
			    top: 4rem;
			    width: 9rem;
			    margin-left: 0.65rem;
	    	.fenshu{
	    		color: red;
	    		font-weight: bold;
	    	}
	    }
	    .pingjia{
	    	color: palevioletred;
		    font-size: 18px;
		    font-weight: bold;
		    position: absolute;
		    top: 5.5rem;
		    text-align: center;
		    margin-left: 0.8rem;
	    }
	}
	/*分数结束*/
	
	/*分享按钮*/
	.share{
		background: url(../assets/4-3.png) no-repeat;
		    background-size: 100% 100%;
		    width: 6rem;
		    height: 3rem;
		    position: absolute;
		    top: 15rem;
		    left: 50%;
		    margin-left: -3rem;
	}

	/*遮罩层*/
	.mask{
		background: url(../assets/5-1.png) no-repeat;
		background-size: 100% 100%;
	    width: 100%;
	    height: 100%;
	    position: absolute;
	    top: 0;
	    bottom: 0;
	    opacity: 0.8;
	    .share_img{
	    	width: 12rem;
		    height: 10rem;
		    position: absolute;
		    top: 0.3rem;
		    left: 50%;
		    margin-left: -6rem;
	    }
	}
</style>