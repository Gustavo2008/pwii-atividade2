<template>
  <div class="container mt-2">
    <div>
      <p style="font-size: 2em; color: darkblue; margin-bottom: 0">
        <strong>Contatos</strong>
      </p>
      <div style="font-size: 0.75em; color: darkblue; justify-content: right">
        <p v-if="numContatos <= 0">Adicione um contato na agenda...</p>
        <p v-else>Há {{ numContatos }} contatos na agenda.</p>
      </div>
    </div>

    <hr />

    <div v-for="(contato, index) in contatos" :key="index">
      <b-card class="mb-2">
        <b-card-text>
          <div
            style="
              position: relative;
              display: flex;
              flex-wrap: wrap;
              align-items: center;
              justify-content: space-between;
              padding: 0.5rem rem 1rem;
            "
          >
            <strong>{{ contato.name }}</strong>
            <strong>{{ contato.number }}</strong>

            <div>
              <button class="btn">
                <img
                  title="Editar contato"
                  href="#"
                  class="mr-2"
                  @click="editar(index)"
                  src="../../public/editar.png"
                  height="30px"
                  width="30px"
                  style="padding: 5px; margin-right: 5px"
                />
              </button>

              <button class="btn">
                <img
                  title="Apagar contato"
                  href="#"
                  class="mr-2"
                  @click="excluir(contato, index)"
                  src="../../public/lixo.png"
                  height="30px"
                  width="30px"
                  style="color: red; padding: 5px; margin-right: 5px"
                />
              </button>
            </div>
          </div>
        </b-card-text>
      </b-card>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  name: "ListaContatos",

  data() {
    return {
      contatos: [],
      selecionado: [],
    };
  },
  created() {
    this.contatos = localStorage.getItem("contatos")
      ? JSON.parse(localStorage.getItem("contatos"))
      : [];
  },
  methods: {
    editar(index) {
      this.$router.push({ name: "cadastrar", params: { index } });
    },
    excluir(contato, index) {
      this.selecionado = contato;
      this.selecionado.index = index;
      this.contatos.splice(this.selecionado.index, 1);
      localStorage.setItem("contatos", JSON.stringify(this.contatos));
    },
  },
  computed: {
    numContatos() {
      return this.contatos.length;
    },
  },
};
</script>
