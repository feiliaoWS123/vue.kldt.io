<template>
	<div>
		<!--头部提示信息-->
		<header class="top_tips">
			<span class="tips_num">题目{{questionNum}}</span>
		</header>
		<!--中间的item，也就是答题部分-->
		<div>
			<div class="question_container common_middle">
				<div class="qutesiton_content">
					<!--题干信息-->
					<header class="question_title">{{questionList[questionNum-1].topic_name}}</header>
					<!--选项信息-->
					<ul class="answer_list">
						<li class="answer_list_item" v-for="(item,index) in questionList[questionNum-1].topic_answer" @click="chooseQu(index,item.topic_answer_id)">
							<!--ABCD-->
							<span class="choose_num" :class="{choosed_num:chooseNum == index}">{{handler(index)}}</span>
							<!--选项-->
							<span class="answer_detail">{{item.answer_name}}</span>
						</li>
					</ul>
				</div>
			</div>
			<div class="next_question common_button_style" v-if="questionNum < questionList.length" @click="next"></div>
			<div class="common_button_style submit" v-else @click="submitHander"></div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return {
				//选项
				chooseNum:null,
				//答案 
				myAnswer:null,
				//题目
				questionNum:this.$store.state.questionNum,
				//题干
				questionList:this.$store.state.questionList,
			}
		},
		methods:{
			//A.B.C.D
			handler:function(index){
				if(index == 0){
					return "A"
				}else if(index == 1){
					return "B"
				}else if(index == 2){
					return "C"
				}else{
					return "D"
				}
			},
			//记录选项和答案
			chooseQu:function(index,id){
				this.chooseNum = index;
				this.myAnswer = id;
			},
			next:function(){
				if(this.chooseNum == null){
					alert("您还未选择呢！");
				}else{
					//默认选项为空
					this.chooseNum = null;
					//展示下一题
					this.questionNum += 1;
					//记录选择的答案
					this.$store.dispatch("myAnswerAction",this.myAnswer);
				}		
			},
			//点击提交判断是否答题情况
			submitHander:function(){
				if(this.chooseNum == null){
					alert("您还未选择呢！");
				}else{
					//跳转到score页面
					this.$router.push("/score");
					this.$store.dispatch("myAnswerAction",this.myAnswer);
				}	
			}
		}
	}
</script>

<style scoped="scoped" lang="less">
	/*头部提示开始*/
	
	.top_tips {
		width: 4rem;
		height: 6rem;
		background: url(../assets/WechatIMG2.png) no-repeat;
		background-size: 100% 100%;
		position: absolute;
		right: 1.5rem;
		.tips_num {
			font-size: 0.65rem;
			display: inline-block;
			width: 3.8rem;
			height: 1.4rem;
			position: absolute;
			top: 4.2rem;
			text-align: center;
			line-height: 1.4rem;
			color: #9F9164;
			font-weight: lighter;
		}
	}
	/*头部提示结束*/
	
	.common_middle {
		width: 12rem;
		height: 10rem;
		position: absolute;
		top: 6rem;
		left: 50%;
		margin-left: -6rem;
	}
	/*答题部分开始*/
	
	.question_container {
		background: url(../assets/2-1.png) no-repeat;
		background-size: 100% 100%;
		.question_title {
			font-size: 0.65rem;
			width: 8rem;
			position: absolute;
			top: 2rem;
			left: 2.5rem;
		}
		.answer_list {
			position: absolute;
			top: 3rem;
			left: 2.5rem;
			.choose_num {
				font-size: 0.6rem;
				display: inline-block;
				border: 1px solid gray;
				width: 0.8rem;
				height: 0.8rem;
				border-radius: 50%;
				text-align: center;
				line-height: 0.8rem;
			}
			.choosed_num {
				border: 1px solid yellow;
				background-color: yellow;
				color: black;
			}
			.answer_detail {
				font-size: 0.6rem;
			}
		}
	}
	
	.common_button_style {
		position: absolute;
		top: 16rem;
		left: 50%;
		margin-left: -2rem;
		width: 4rem;
		height: 2rem;
	}
	
	.next_question {
		background: url(../assets/2-2.png) no-repeat;
		background-size: 100% 100%;
	}
	
	.submit {
		background: url(../assets/3-1.png) no-repeat;
		background-size: 100% 100%;
	}
	/*答题部分结束*/
</style>