<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
        <form id="pizza-form" @submit="createPizza">
            <div class="input-container">
                <label for="nome">Nome do cliente:</label>
                <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite se nome">
            </div>
            <div class="input-container">
                <label for="sabor">Escolha o sabor</label>
                <select name="sabor" id="tipo" v-model="sabor">
                    <option value="">Selecione o sabor</option>
                    <option v-for="sabor in sabores" :key="sabor.id" :value="sabor.tipo">
                        {{ sabor.tipo }}
                    </option>
                </select>
            </div>
            <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="opcionais">Escolha os opcionais:</label>
                <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                    <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                    <span>{{ opcional.tipo }}</span>
                </div>
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Finalizar Pedido">
            </div>
        </form>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
    name: "PizzaForm",
    data() {
        return {
            sabores: null,
            opcionaisdata: null,
            nome: null,
            sabor: null,
            opcionais: [],
            msg: null
        }
    },
    // Pegando o cardápio:
    methods: {
        async getCardapio() {
            const req = await fetch("http://localhost:3000/Cardapio");
            const data = await req.json();
            
            this.sabores = data.sabores;
            this.opcionaisdata = data.opcionais
        },
        // Enviando os dados para o backend  como um Post - (submit do usuário):
        async createPizza(e) {
            // e.preventDefault();

            const data = {
                nome: this.nome,
                sabor: this.sabor,
                opcionais: Array.from(this.opcionais),
                status: "Solicitada",
            }
            // Inserindo o pedido no banco:
            const dataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/pizzas", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();
            
            // colocando uma msg do sistema:
            this.msg = `Seu pedido foi realizado(Pedido Nº ${res.id})`;
            
            // limpar mensagem após 3s:
            setTimeout(() => this.msg = "",3000);
            
            // limpando os campos após preencher e fazer o pedido:
            this.nome = "";
            this.sabor = "";
            this.opcionais = ""
        }
    },
    mounted() {
        this.getCardapio()
    },
    components: { Message }
}
</script>

<style scoped>
    #pizza-form {
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container {
        display: flex;
        flex-direction: column; /* A label fica em uma linha e o input na outra */
        margin-bottom: 22px
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: rgb(0, 47, 0);
        padding: 5px 10px;
        border-left: 5px solid  rgb(211, 6, 6);
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px
    }
    
    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 5px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: rgb(211, 6, 6);
        color: #fff;
        font-weight: bold;
        border: 2px solid rgb(211, 6, 6);
        padding: 10px;
        font-size: 17px;
        margin: 0 auto;
        cursor: pointer;
        border-radius: 10px;
        transition: 0.5;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: rgb(211, 6, 6);
        transition: 0.5s;
    }
</style>