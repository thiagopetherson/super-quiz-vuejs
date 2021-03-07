<template>
    <div class="result" :class="{wrong: !result}">
        <span v-if="result">Resposta Certa! :)</span>
        <span v-else>Resposta Errada! :(</span>
        <!-- Ali, naquele evento, estamos ativando o evento 'confirmed', que confirma que o usuário viu o resultado -->
        <hr>
        <button @click="$emit('confirmed')">Próxima Pergunta</button>
    </div>
</template>

<script>
export default {
    props: {        
        result: {
            type: Boolean, //Diz se a questão é opção certa ou errada
            required: true
        }
    }
}
</script>

<style>

    /* Classe para quando estiver certo (por padrão) */
    .result {
        height: 400px;
        color: #000;
        background-color: #FFF;
        width: 70%;
        border-radius: 20px;
        font-size: 5.5rem;

        display: flex;
        flex-direction: column;
        justify-content: center;
        background-color: #89c454;
        color: #30863d;
    }

    .result hr {
        color: #FFF;
    }

    /* Classe para quando estiver errado */
    .result.wrong {
        background-color: #f05250;
        color: #bb2814;
    }

    /* Classe para quando o botão estiver dentro de uma resposta certa */
    .result button {
        outline: none;
        align-self: center;
        padding: 10px 20px;
        font-size: 1.7rem;
        border-radius: 8px;
        background-color: #FFF;
        color: #30863d;
        font-weight: 600;
    } 

    /* Classe para quando o botão estiver dentro de uma resposta errada */
    .result.wrong button {
        color: #bb2814;
    }
</style>
