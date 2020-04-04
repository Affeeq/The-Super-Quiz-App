<template>
	<div class="panel panel-default">
		<div class="panel-heading">
			<h3 class="panel-title">What's {{ firstNum }} {{ mode }} {{ secondNum }}?</h3>
		</div>
		<div class="panel-body">
			<transition-group name="fade" appear>
				<div class="col-xs-6" v-for="(choice,index) in choices" :key="choice">
					<button class="btn btn-primary" @click.prevent="checkAnswer(choice)">{{ choice }}</button>
				</div>
			</transition-group>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				localSelectedComponent: this.selectedComponent,
				answerPos: '',
				mode: '',
				firstNum: '',
				secondNum: '',
				answer: '',
				firstChoice: '',
				secondChoice: '',
				thirdChoice: '',
				fourthChoice: '',
				choices: ['', '', '', '']
			};
		},
		methods: {
			checkAnswer(value) {
				if (value == this.answer) {
					this.localSelectedComponent = 'app-success';
					this.$emit('answerChecked', this.localSelectedComponent);
				} else {
					alert('Try again!');
				}
			},
			randomNum(max, min) {
				return (Math.floor(Math.random() * (max - min + 1)) + min);
			},
			correctAnswerPos() {
				return this.answerPos = this.randomNum(4, 1);
			},
			firstQuestionNum() {
				return this.firstNum = this.randomNum(0, 100);
			},
			secondQuestionNum() {
				return this.secondNum = this.randomNum(0, 100);
			},
			choicesAnswer() {
				let old = [];
				for (let [index, choice] of this.choices.entries()) {
					if (index == (this.answerPos - 1)) {
						this.choices[index] = this.answer;
					} else {
						let random = this.randomNum(10, 1);
						if (this.randomNum(1, 0) > 0.5) {
							if ( old.includes(this.answer + random)) {
								do {
									random = this.randomNum(10, 1);
								} while (old.includes(this.answer + random));
								this.choices[index] = this.answer + random;
							} else {
								this.choices[index] = this.answer + random;
								old.push(this.choices[index]);
							}
						} else {
							if (old.includes(this.answer - random)) {
								do {
									random = this.randomNum(10, 1);
								} while (old.includes(this.answer - random));
								this.choices[index] = this.answer - random;
							} else {
								this.choices[index] = this.answer - random;
								old.push(this.choices[index]);
							}
						}
					}
				}
			},
			randomMode() {
				if (this.randomNum(1, 0) > 0.5) {
					this.mode = '+';
				} else {
					this.mode = '-';
				}
			}
		},
		beforeMount() {
			this.correctAnswerPos();
			this.firstQuestionNum();
			this.secondQuestionNum();
			this.randomMode();
			this.correctAnswer;
			this.choicesAnswer();
		},
		computed: {
			correctAnswer() {
				if (this.mode == '+') {
					return this.answer = this.firstNum + this.secondNum;
				} else {
					return this.answer = this.firstNum - this.secondNum;
				}
			}
		},
		props: ['selectedComponent']
	}
</script>

<style>
	.btn {
    	margin: 5px 0;
  	}

  	.fade-enter {
        opacity: 0;
    }

    .fade-enter-active {
        transition: opacity 1s;
    }

    .fade-leave {
        /*opacity: 1s;*/
    }

    .fade-leave-active {
        transition: opacity 1s;
        opacity: 0;
    }
</style>