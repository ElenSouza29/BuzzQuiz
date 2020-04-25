<template>
  <div class='container'>
    <div class="columns is-8 tile is-vertical" data-test='pergunta' v-for="(item, indexPergunta) in quiz" :key="item.pergunta">
      <div class="column">
        <nav  class="level box-pergunta">
            <p class="level-item has-text-centered">{{item.pergunta}}</p>
        </nav>
      </div> 
      <div class="column" data-test="opcao" v-for="(respostas, indexResposta) in item.resposta" :key="respostas">
                <button 
                    :data-resposta="validaResposta(indexPergunta,indexResposta)" v-on:click="incluirResposta(indexResposta,indexPergunta)"
                    :class="{ 'is-success': respostaCerta( indexPergunta, indexResposta ), 'is-danger': respostaErrada( indexPergunta, indexResposta ) }" v-bind:teste="item.indexPergunta"
                    :disabled="verificaRespondida(indexPergunta)"   class="button is-large is-fullwidth">{{respostas}}
                </button>
        </div> 
    </div>
    <div class="columns">
        <div class="column is-8">
            <nav :data-resultado="numeroAcertos" class="level box-rodape">
                <p  class="level-item has-text-centered">Você acertou {{numeroAcertos}} capitais</p>
                <button data-test="refazer" @click="zerarQuiz" class="button is-light is-medium refazer">Refazer</button>
            </nav>
        </div>
    </div>    
  </div>
</template>
<script>
export default {
    data() {
        return {
            quiz: [
                    {   pergunta: "Qual a capital de Argentina?",
                        resposta: ["Mendoza", "Buenos Aires", "Bariloche", "Ushuaia"],
                        indexRespostaEscolhida: null,
                        indexRespostaCerta: 1   
                    },
                    {   pergunta: "Qual a capital do Brasil?",
                        resposta: ["Bahia", "São Paulo", "Brasília", "Rio de Janeiro"],
                        indexRespostaEscolhida: null,
                        indexRespostaCerta: 2  
                    },
                    {   pergunta: "Qual a capital de Uruguai?",
                        resposta: ["Punta Del Leste", "Colônia de Sacramento", "Salto", "Montevidéu"],
                        indexRespostaEscolhida: null,
                        indexRespostaCerta: 3  
                    },
                    {   pergunta: "Qual a capital dos Estados Unidos?",
                        resposta: ["Washington", "New York", "Colorado", "Las Vegas"],
                        indexRespostaEscolhida: null,
                        indexRespostaCerta: 0
                    }
            ]
        }
    },

    computed: {
        numeroAcertos() {
            let count = 0;
            this.quiz.forEach(item => {
                if(item.indexRespostaEscolhida === item.indexRespostaCerta) {
                    count++
                }
            })
            return count;
        },
    },

    methods: {

        incluirResposta: function(indexR,indexP) {
            this.quiz[indexP].indexRespostaEscolhida = indexR;
            this.validaResposta(indexR,indexP);
        },

        respostaCerta: function( indexP, indexR) {
            let respostaCerta = this.quiz[indexP].indexRespostaCerta;
            return (respostaCerta === indexR &&
                   this.quiz[indexP].indexRespostaEscolhida != null);
        },

        respostaErrada: function( indexP, indexR ) {
            let respostaEscolhida = this.quiz[indexP].indexRespostaEscolhida;
            let respostaCerta = this.quiz[indexP].indexRespostaCerta;
            return (respostaEscolhida === indexR &&
                    respostaEscolhida != null && respostaCerta != indexR);
        },

        verificaRespondida: function (indexP) {
            return this.quiz[indexP].indexRespostaEscolhida != null;
        },

        zerarQuiz: function() {
            this.quiz.forEach(item => (item.indexRespostaEscolhida = null));
        },

        validaResposta: function(indexP, indexR) {
            let respostaCerta = this.quiz[indexP].indexRespostaCerta;
            let statusResposta = "errada";
                if (respostaCerta === indexR && this.quiz[indexP].indexRespostaEscolhida != null) {
                    statusResposta = "correta";
                }
            return statusResposta;
            }

    }
}
</script>

<style>

.box-pergunta {
    background: rgba(0, 0, 0, 0.4);
    height: 200px;
    font-size: 40px;
    color: white;
    font-weight: bold;
}

.box-rodape {
    background: black;
    height: 100px;
    padding: 20px;
    font-size: 40px;
    color: white;
    font-weight: bold;
}
</style>