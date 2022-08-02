<template>
  <!--Aqui tenho a navegação superior da página-->
  <div id="app" style="font-size: 1.2em">
    <b-navbar toggleable="lg" type="dark" variant="primary">
      <b-navbar style="justify-content: center"
        ><strong style="justify-content: center; font-size: 1.5em"
          >Agenda Telefonica</strong
        ></b-navbar
      >

      <b-collapse id="nav-collapse" style="justify-content: right" is-nav>
        <b-navbar-nav>
          <b-nav-item to="/"
            ><img
              title="Listar contato"
              href="#"
              class="mr-2"
              @click="editar(index)"
              src="../public/listar.png"
              height="30px"
              width="30px"
              alt="Imagem de uma agenda"
          /></b-nav-item>
          <b-nav-item to="/cadastrar"
            ><img
              title="Adicionar contato"
              href="#"
              class="mr-2"
              @click="editar(index)"
              src="../public/adicionar.png"
              height="30px"
              width="30px"
              alt="Imagem de uma agenda"
          /></b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <router-view />
  </div>
</template>
