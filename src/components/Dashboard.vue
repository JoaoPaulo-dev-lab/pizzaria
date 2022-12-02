<template>
  <div id="pizza-table">
    <Message :msg="msg" v-show="msg" />
    <div>
        <div id="pizza-table-heading">
            <div class="order-id">#:</div>
            <div>Clientes</div>
            <div>Sabor:</div>
            <div>Opcionais:</div>
            <div>Ações:</div>
        </div>
    </div>
    <div id="pizza-table-rows">
        <div class="pizza-table-row" v-for="pizza in pizzas" :key="pizza.id">
            <div class="order-number">{{pizza.id}}</div>
            <div>{{ pizza.nome }}</div>
            <div>{{ pizza.sabor }}</div>
            <div>
                <ul>
                    <li v-for="(opcional, index) in pizza.opcionais" :key="index">
                        {{opcional}}    
                    </li>
                </ul>
            </div>
            <div>
                <select name="status" class="status" @change="updatePizza($event, pizza.id)">
                    <option value="">Selecione</option>
                    <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="pizza.status == s.tipo">
                        {{ s.tipo }}
                    </option>
                </select>
                <button class="delete-btn" @click="deletePizza(pizza.id)">Cancelar</button>
            </div>
        </div>        
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
    name: "Dashboard",
    data() {
        return {
            pizzas: null,
            pizza_id: null,
            status: [],
            msg: null
        }
    },
    components: { Message },
    
    methods: {
        async getPedidosView() {
            const req = await fetch("http://localhost:3000/pizzas");
            const data = await req.json();
            this.pizzas = data;

            // Resgatando os status:
            this.getStatus();
        },

        async getStatus() {
            const req = await fetch("http://localhost:3000/status");
            const data = await req.json();
            this.status = data;
        },
        // Implementando 'Cancelar os pedidos':
        async deletePizza(id) {
            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: "DELETE"
            });
            const res = await req.json();

            // colocando uma msg do sistema de que o pedido foi deletado:
            this.msg = `Pedido removido!`;
            
            // limpar mensagem após 3s:
            setTimeout(() => this.msg = "",3000);
            this.getPedidosView();
        },
        async updatePizza(event, id) {
            //Pegando a opção que o usuário selecionou:
            const option = event.target.value;
            //Colocando em string o json de status para atualizar no banco de dados: 
            const dataJson = JSON.stringify({ status: option });
            // Acessando o pedido pelo 'id' e atualizando o status dele: 
            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json()

            // colocando uma msg do sistema de atualização do status do pedido:
            this.msg = `O pedido Nº ${res.id} foi atualizado para "${res.status}"!`;
            
            // limpar mensagem após 3s:
            setTimeout(() => this.msg = "",5000);
            console.log(res)
        }
    },
    mounted() {
        this.getPedidosView()
    }
}
</script>

<style scoped>
    #pizza-table {
        max-width: 1200px;
        margin: 0 auto;
    }

    #pizza-table-heading,
    #pizza-table-rows,
    .pizza-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #pizza-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid rgb(211, 6, 6);
    }

    #pizza-table-heading div,
    .pizza-table-row div {
        width: 20%;
    }

    .pizza-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #pizza-table-heading .order-id,
    .pizza-table-row .order-number {
        width: 5%;
    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
    }

    .delete-btn {
        background-color: rgb(211, 6, 6);
        color: #fff;
        font-weight: bold;
        border: 2px solid rgb(211, 6, 6);
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
        border-radius: 5px;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: rgb(211, 6, 6);
    }

</style>