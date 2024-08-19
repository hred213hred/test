<template>
	<div class="keyboard">
					<button class="action-button" @click="allClean">AC</button>
					<button class="action-button" @click="squareRoot('√')">√</button>
					<button class="action-button" @click="calcPercent">%</button>
					<button class="action-button" @click="addOperator('/')">÷</button>

					<button class="number-button" @click="addNumber">7</button>
					<button class="number-button" @click="addNumber">8</button>
					<button class="number-button" @click="addNumber">9</button>
					<button class="action-button" @click="addOperator('*')">×</button>

					<button class="number-button" @click="addNumber">4</button>
					<button class="number-button" @click="addNumber">5</button>
					<button class="number-button" @click="addNumber">6</button>
					<button class="action-button" @click="addOperator('-')">-</button>

					<button class="number-button" @click="addNumber">1</button>
					<button class="number-button" @click="addNumber">2</button>
					<button class="number-button" @click="addNumber">3</button>
					<button class="action-button" @click="addOperator('+')">+</button>

					<button  class="number-button" @click="addNumber">0</button>
					<button class="number-button" @click="addNumber">.</button>
					<button class="action-button" @click="deleteLastSymbol">del.</button>
					<button class="action-button" @click="showResult">=</button>
	</div>
	</template>

<script>
export default {
	data() {
		return{
			value: '',
			shadowValue:'',
			memory:[],
			operators:['+','-', '*', '/'],
			numbers:['1','2','3','4','5','6','7','8','9','0','.']
		}
	},

	methods:{
		addNumber(event){
			this.value += event.target.textContent
			this.shadowValue += event.target.textContent
				this.$emit('addNumber', {
					addNumber: this.value
			})
		},

		deleteLastSymbol(){
			console.log(this.memory)

			if(this.memory.length === 1){
				this.memory =[]
			}
			for(let i=0; i <= this.numbers.length; i++){
				if(this.value[this.value.length-1] === this.numbers[i]){
					this.value = this.value.slice(0,-1)
					this.shadowValue = this.shadowValue.slice(0,-1)
				}
			}
			for(let i=0; i <= this.operators.length; i++){
				if(this.memory[this.memory.length-1] === this.operators[i] && this.shadowValue === ''){
					this.memory.pop()
					this.value = this.value.slice(0,-1)
				}
			}

			console.log(this.memory)

			this.$emit('deleteLastSymbol', {
				deleteLastSymbol:this.value
			})
		},

		addOperator(oper){
			if(this.shadowValue !== ''){
				this.memory.push(this.shadowValue)
			}
			this.value += oper
				for(let i=0; i <= this.memory.length; i++){
					if(this.memory[i] === this.operators[0]){
						let res = Number(this.memory[i-1]) + Number(this.memory[i+1])
						this.shadowValue = res
						this.memory=[]
						this.memory.push(res)
					}else if(this.memory[i] === this.operators[1]){
						let res = Number(this.memory[i-1]) - Number(this.memory[i+1])
						this.shadowValue = res
						this.memory=[]
						this.memory.push(res)
					}else if(this.memory[i] === this.operators[2]){
						let res = this.memory[i-1] * this.memory[i+1]
						this.shadowValue = res
						this.memory=[]
						this.memory.push(res)
					}else if(this.memory[i] === this.operators[3]){
						let res = this.memory[i-1] / this.memory[i+1]
						this.shadowValue = res
						this.memory=[]
						this.memory.push(res)
					}
				}
			this.memory.push(oper)
			this.shadowValue = ''

			console.log(this.memory)

			this.$emit('addOperator', {
				addOperator: this.value
			})
		},

		calcPercent(){
			this.shadowValue = this.memory[0] * this.shadowValue / 100
			this.memory.push(this.shadowValue)
			for(let i=0; i<=this.operators.length; i++){
				if(this.memory[i] === this.operators[0]){
					let res = Number(this.memory[i-1]) + Number(this.memory[i+1])
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}else if(this.memory[i] === this.operators[1]){
					let res = Number(this.memory[i-1]) - Number(this.memory[i+1])
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}else if(this.memory[i] === this.operators[2]){
					let res = Number(this.memory[i-1]) * Number(this.memory[i+1] / 100)
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}else if(this.memory[i] === this.operators[3]){
					let res = Number(this.memory[i-1]) / Number(this.memory[i+1] / 100)
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}
			}
			this.$emit('calcPercent', {
				calcPercent: this.value
			})
		},

		showResult(){
			this.memory.push(this.shadowValue)
			for(let i=0; i <= this.memory.length; i++){
				if(this.memory[i] === this.operators[0]){
					let res = Number(this.memory[i-1]) + Number(this.memory[i+1])
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}else if (this.memory[i] === this.operators[1]){
					let res = Number(this.memory[i-1]) - Number(this.memory[i+1])
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}else if (this.memory[i] === this.operators[2]){
					let res = this.memory[i-1] * this.memory[i+1]
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}else if (this.memory[i] === this.operators[3]){
					let res = this.memory[i-1] / this.memory[i+1]
					this.value = res
					this.shadowValue = res
					this.memory=[]
					this.memory.push(res)
				}
			}
			this.$emit('showResult', {
				showResult: this.value
			})
		},

		allClean(){
			this.memory = []
			this.value = ''
			this.shadowValue = ''
			this.$emit('allClean', {
				allClean: this.value
			})
		},
    // TODO: функция eval не должна использоваться в коде
		squareRoot(){
			this.value = Math.sqrt(this.value);
			this.shadowValue = this.value;
			this.memory.push(this.shadowValue)
			this.$emit('squareRoot', {
				squareRoot: this.value
			})
		},
	}
}
</script>

<style lang="scss" scoped>
.keyboard{
	width: 100%;
	height:auto;
	margin-top: 1px;
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	grid-gap: 1px;
	grid-template-rows:repeat(5, 30px);
	.action-button{
		color: black;
		padding: 0;
		background: rgb(255, 190, 116);
		cursor:pointer;
		border-width: 1px;
	}
	.number-button{
		color: black;
		padding: 0;
		background: rgb(172, 172, 172);
		cursor:pointer;
		border-width: 1px;
	}
}
</style>