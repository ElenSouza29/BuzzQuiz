<template>
  <div id="app">
    <div class="container">
      <div class="columns">
          <div class="column is-8">
            <div class='tile is-parent'>
              <article class='tile is-child notification is-info'>
                <p class='title'>Você consegue reconhecer as capitais desses países? </p>
                <p class='subtitle'>Eu sei que você é capaz!</p>
              </article>
            </div>
          </div>
        </div>
        <perguntas></perguntas>
    </div>
  </div>
</template>

<script>
  import Perguntas from "./components/Perguntas";
  export default {
    name: "App",
    components: {Perguntas}
  };
</script>

<style lang="scss">
  @import "../node_modules/bulma/bulma.sass";
  
</style>