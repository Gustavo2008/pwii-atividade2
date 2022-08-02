<template>
  <div class="container mt-2">
    <div>
      <p style="font-size: 2em; color: darkblue">
        <strong>Novo contato</strong>
      </p>
    </div>
    <hr />
    <b-form>
      <b-form-group label-for="name">
        <b-form-input
          id="name"
          v-model="form.name"
          type="text"
          placeholder="Nome"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group label-for="number">
        <b-form-input
          id="number"
          v-model="form.number"
          type="number"
          placeholder="Telefone"
          required
          max="999999999"
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="outline-primary" @click="salvarContato"
        >Salvar</b-button
      >
    </b-form>
  </div>
</template>
<script>
export default {
  name: "Cadastrar",

  data() {
    return {
      form: {
        name: "",
        number: "",
      },
      metodoSalvar: "novo",
    };
  },

  created() {
    if (
      this.$route.params.index === 0 ||
      this.$route.params.index !== undefined
    ) {
      this.metodoSalvar = "atualizar";
      let contatos = JSON.parse(localStorage.getItem("contatos"));
      this.form = contatos[this.$route.params.index];
    }
  },
  methods: {
    salvarContato() {
      if (this.form.name === "" || this.form.number === "") {
        this.$router.push({ name: "listacontatos" });
        return;
      } else if (this.metodoSalvar === "atualizar") {
        let contatos = JSON.parse(localStorage.getItem("contatos"));
        contatos[this.$route.params.index] = this.form;
        localStorage.setItem("contatos", JSON.stringify(contatos));
        this.$router.push({ name: "listacontatos" });
        return;
      }
      let contatos = localStorage.getItem("contatos")
        ? JSON.parse(localStorage.getItem("contatos"))
        : [];
      contatos.push(this.form);
      localStorage.setItem("contatos", JSON.stringify(contatos));
      this.$router.push({ name: "listacontatos" });
    },
  },
};
</script>
