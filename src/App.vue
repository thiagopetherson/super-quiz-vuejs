<template>
	<div id="app">
		<h1>Super Quiz</h1>
		<transition name="flip" mode="out-in">
			<!-- Ali no :question estamos passando a questão para o componente -->
			<Question v-if="questionMode" :question="questions[currentQuestion]" @answered="showResult($event)"></Question> 
			<!-- Ali no :result estamos passando o resultado para o componente -->
			<Result v-else :result="result" @confirmed="nextQuestion"></Result> 
		</transition>
	</div>
</template>

<script>
import questions from './util/questions.js' //Importando o array de questões
import Question from './components/Question.vue' //Importando o componente Question
import Result from './components/Result.vue' //Importando o componente Result

export default {
	components: { Question, Result },
	data() {
		return {
			result: false, //Inicialmente será falso (essa propriedade armazenará se o usuário respondeu certo ou errado)
			questionMode: true, //Mostra a questão ou o resultado 
			questions:questions, //Pegando aquele array que foi importado e colocando dentro do componente (poderia ser colocado só uma vez 'questions')
			currentQuestion: 0, //Índice da questão corrente. Da questão selecionada
		}
	},
	methods: {
		showResult(result) {
			this.result = result, //Aqui vamos dizer se a resposta foi certa ou errada
			this.questionMode = false //Aqui é pra dizer que queremos mostrar o resultado
		},
		nextQuestion() {			
			//Abaixo, estamos selecionando de maneira aleatório a pergunta que irá cair
			let r = Math.random() * this.questions.length
			this.currentQuestion = parseInt(r),
			//Aqui estamos dizendo que queremos mostrar a pergunta (ao invés do resultado)
			this.questionMode = true
		}

	}
}
</script>

<style>
body {
	background: linear-gradient(to right, rgb(0, 0, 70), rgb(28, 181, 224));
	font-family: 'Oswald', sans-serif;
	color: #FFF;
	height: 100vh;
}

#app {
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;

	display: flex;
	flex-direction: column;
	align-items: center;
}

#app h1 {
	font-weight: 200;
	font-size: 4rem;
}

/* Adicionando animação */
@keyframes flip-out { /* Fazendo a rotação no elemento */
	from { transform: rotateY(0deg); }
	to { transform: rotateY(90deg); }
}

@keyframes flip-in { /* Desfazendo a rotação no elemento */
	from { transform: rotateY(90deg); }
	to { transform: rotateY(0deg); }
}

.flip-enter-active { /* Aplicando a animação na entrada do elemento */
	animation: flip-in 0.3s ease;
}

.flip-leave-active { /* Aplicando a animação na saída do elemento */
	animation: flip-out 0.3s ease;
}
</style>
