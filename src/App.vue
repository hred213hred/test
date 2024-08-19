<template>
		<main>
			<div class="wrapper">
				<input class="word" v-model="inputValue" placeholder="0" />
			</div>
			<the-button 
			@addNumber="addNumber"
			@allClean="allClean"
			@addOperator="addOperator"
			@showResult="showResult"
			@squareRoot="squareRoot"
			@calcPercent="calcPercent"
			@deleteLastSymbol="deleteLastSymbol"
			></the-button>
		</main>
</template>
<!--          TODO: Сделай переиспользуемый компонент кнопки, компоненты хранятся в папке components #--> 


<script>
import TheButton from './components/TheButton.vue'
export default{
  // TODO: Убери неиспользуемый код (комментарии)#
	components:{
		TheButton,
	},
	data(){
		return{
			inputValue:'',
		}
	},
	methods:{
		addNumber(data){
			this.inputValue = Object.values(data)
		},

		allClean(){
			this.inputValue = ''
		},

		addOperator(data){
			this.inputValue = Object.values(data)
		},

		showResult(data){
			this.inputValue = Object.values(data)
		},

		squareRoot(data){
			this.inputValue = Object.values(data)
		},

		calcPercent(data){
			this.inputValue = Object.values(data)
		},

		deleteLastSymbol(data){
			this.inputValue = Object.values(data)
		}
		// TODO: Пробелы не нужны после объявления методов (+ if else конструкции (else пишется на той же строке, где заканчивается if)#)
    // TODO: Между методами 1 вместо 2
	},

// TODO: Убери ненужные пробелы#
}
</script>
<!--TODO: Стили пишутся везде с атрибутом scoped #-->
<!-- /* TODO: Сделай для одной страницы названия классов в стиле БЭМ +
добавь в тег style атрибут lang="scss", используя препроцессор, перепиши стили для калька
*/ -->
<style lang="scss" scoped>

	@mixin wh ($w, $h){
		width:$w;
		height:$h;
	}
	html{
	@include wh(100%, 100%)
	}
	body{
		@include wh(100%, 100%);
		box-sizing: content-box
	}
	#app{
		@include wh(100%, 100%)
	}
	main{
		max-width:25%;
		min-width: 120px;
		margin: 150px auto;
		.wrapper{
			@include wh(100%, 50px);
			padding: 0;
		}
		.word{
			@include wh(100%, 100%);
			margin: 0;
			box-sizing: border-box;
			padding: 2px;
			border: 1px solid black;
			background-color: black;
			color:white;
			font-size: large;
		}
	}
	@media (max-width:700px){
			main{
				max-width: 120px;
			}
		}
</style>