<template>
  <div id="app">
    <b-navbar type="dark" variant="dark" class="justify-content-center">
      <b-navbar-brand to="/" class="mx-0"><h1>Carta Virtual</h1></b-navbar-brand>      
    </b-navbar>
  
    <router-view/>  

  </div>
</template>

<style lang="scss">

  html, #app {
    background-color: #212529;
  }

  .backgroud-bar{
    background-color: rgb(255, 99, 71);

    h1{
      color:white;
      text-shadow: 2px 2px 5px black;
      padding: 0.2em 0;
      text-align: center;
      font-size: 2.5em;
    }
  }

  

</style>
