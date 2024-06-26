<template>
    <div id="burger-table" v-if="burgers">
        <Message :msg="msg" v-show="msg" />
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#</div>
                <div>Cliente</div>
                <div>Pão</div>
                <div>Carne</div>
                <div>Opcionais</div>
                <div>Ações</div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div
                class="burger-table-row"
                v-for="burger in burgers"
                :key="burger.id"
            >
                <div class="order-number">{{ burger.id }}</div>
                <div>{{ burger.nome }}</div>
                <div>{{ burger.pao }}</div>
                <div>{{ burger.carne }}</div>
                <div>
                    <ul
                        v-for="(opcional, index) in burger.opcionais"
                        :key="index"
                    >
                        <li>{{ opcional }}</li>
                    </ul>
                </div>
                <div>
                    <select
                        name="status"
                        class="status-select"
                        @change="updateBurger($event, burger.id)"
                    >
                        <option
                            :value="s.tipo"
                            v-for="s in status"
                            :key="s.id"
                            :selected="burger.status == s.tipo"
                        >
                            {{ s.tipo }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">
                        Cancelar
                    </button>
                </div>
            </div>
        </div>
    </div>
    <div v-else>
        <h2>Não há pedidos no momento!</h2>
    </div>
</template>

<script>
import Message from "./Message.vue";

export default {
    name: "Dashboard",
    data() {
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: null,
        };
    },
    components: {
        Message,
    },
    methods: {
        async getPedidos() {
            const req = await fetch("http://localhost:3000/burgers");

            const data = await req.json();

            this.burgers = data;

            // Resgata os status de pedidos
            this.getStatus();
        },
        async getStatus() {
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;
        },
        async deleteBurger(id) {
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE",
            });

            const res = await req.json();

            // Remove pedidos.
            this.msg = `Pedido foi removido com sucesso!`;

            // limpar msg
            setTimeout(() => (this.msg = ""), 3000);

            this.getPedidos();
        },
        async updateBurger(event, id) {
            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson,
            });

            const res = await req.json();

            // Atualiza status dos pedidos.
            this.msg = `O pedido Nº ${res.id} foi atualizado para ${res.status}!`;

            // limpar msg
            setTimeout(() => (this.msg = ""), 3000);

            console.log(res);
        },
    },
    mounted() {
        this.getPedidos();
    },
};
</script>

<style scoped>
#burger-table {
    max-width: 100%;
    width: 100%;
    padding-left: 1em;
    padding-right: 1em;
    margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
    display: flex;
    flex-wrap: wrap;
    margin-left: 2px;
    max-width: 100%;
}

#burger-table-heading {
    font-weight: bold;
    padding: 0.75rem;
    max-width: 100%;
    border-bottom: 3px solid #333;
}

.burger-table-row {
    width: 100%;
    padding: 1rem;
    border-bottom: 1px solid #ccc;
}

#burger-table-heading div,
.burger-table-row div {
    width: 19%;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
    width: 5%;
}

select {
    padding: 0.75rem 0.375rem;
    margin-right: 0.75rem;
    max-width: 100%;
}

ul {
    list-style-type: none;
}

.delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 0.125rem solid #222;
    padding: 0.625rem;
    font-size: 1rem;
    margin: 0 auto;
    cursor: pointer;
    transition: 0.5s;
}

.delete-btn:hover {
    background-color: transparent;
    color: #222;
}

@media (max-width: 600px) {
    #burger-table {
        max-width: 100%;
        width: 100%;
    }

    #burger-table-heading div,
    .burger-table-row div {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        max-width: 100%;
    }

    #burger-table-heading .order-id,
    .burger-table-row .order-number {
        width: 5%;
        flex-wrap: wrap;
        word-wrap: break-word;
        gap: 10px;
    }

    #burger-table-heading {
        font-size: 1rem;
        padding: 0.5rem;
    }

    .burger-table-row {
        margin: 2px;
    }
}
</style>
