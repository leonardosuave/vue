<template>
<!--Aqui vai apenas um elemento HTML por componente (Para mais de um elemento adicionar tudo dentro de uma DIV)-->

    <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
        <h2>Componente aqui!</h2>

        <!--Data binding 
        (One way - apenas leitura de variavel) - Não sera modificado o h3 caso modifique este input
        <input type="text" :value="nome"> <br>-->
        
        <!--Two Way - Modifica os valores das var utilizados no HTML
        <input type="text" v-model="descricao">-->

        <h3>{{ cliente.nome }}</h3>
        <p>Email: {{cliente.email}}</p>
        <p>Email: {{ tudoMaiusculo }}</p> <!--Ver email tudo em maiusculo-->
        <p v-if="showIdade">Idade: {{cliente.idade}}</p>
        <p v-else>Idade: desconhecida</p>
        <p v-show="showTel">Tel: {{cliente.tel}}</p>
        <button @click="mudarCor()">Mudar Cor</button>
        <button @click="emitirEvetoDelete()">Deletar</button>
        <h4>Id especial: {{idEspecial}}</h4> <!--Exemplo de computed properties-->

    </div>
    
</template>

<script>
//Aqui pode ser importado outros componentes conforme o import na APP.vue

export default {

    //Exemplo de reatividade - (Semelhante a EJS)
    //String deve ser em aspas duplas e a var vai em duplo colchete.
    data() {
        return {
            //nome: "Leonardo", ->Foi utiizado como Props
            //email: 'leonardo.suave15@hotmail.com', -> Foi utilizado como Props
            //descricao: "Olá, me chamo ....."
            isPremium: true
            }
        },
        props: {
            //Para prop de edição no import do componente
            nome: String,   
            email: String,
            idade: Number,

            //Para prop com objeto
            cliente: Object,
            
            //Para condição v-if
            showTel: Boolean,
            showIdade: Boolean
        },
        methods: {
            mudarCor: function() {
                this.isPremium = !this.isPremium;
            },
            emitirEvetoDelete() {
                console.log('Emitindo do filho!')
                this.$emit('meDelete', {idDoCliente: this.cliente.id, curso: 'Estudos Node.js e Vue.js', emPromocao: true, component: this})
            }
        },
        computed:{ //Sempre retorna um valor
            tudoMaiusculo() {
                return this.cliente.email.toUpperCase()
            },
            idEspecial() {
                return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase()
            }
            
        }
    
}
</script>

<style scoped>
/* Estilo apenas para esse componente */

    .cliente {
        color: brown;
        text-align: center;
    }

    .cliente-premium {
        color: blue;
        text-align: center;
    }


</style>