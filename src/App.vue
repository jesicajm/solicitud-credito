<template>
  <the-navegation></the-navegation>
  <main>
    <formulario-credito></formulario-credito>
  </main>
</template>

<script>
import TheNavegation from './components/TheNavegation.vue';
import FormularioCredito from './components/FormularioCredito.vue';

export default {
  name: 'App',
  components: {
    TheNavegation,
    FormularioCredito
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap');

* {
    box-sizing: border-box;
}

html {
   height: 100%;
}

body { 
    /*background-color: #f7f7f7;*/
    font-family: 'Oswald', Helvetica, sans-serif;
    margin: 0;
    display: grid;
    grid-template-rows: 4.2rem auto;
    grid-template-areas: "header"
                          "main";
    height: 100%;
}

main {
    grid-area: main;
    padding-top: 6.6rem;
}


@media (min-width: 22rem){
    main {
        padding-top: 5rem; 
    }
}

</style>

