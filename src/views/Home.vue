<template>
  <div class="home">

    <b-carousel
      id="carousel-1"
      v-model="slide"
      :interval="4000"
      controls
      indicators
      fade
      background="#ababab"
      img-width="400"
      img-height="300"
      style="text-shadow: 1px 1px 2px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      
      <b-carousel-slide img-src="https://picsum.photos/1024/300/?image=195"></b-carousel-slide>

      <b-carousel-slide img-src="https://picsum.photos/1024/300/?image=192"></b-carousel-slide>
      
      <b-carousel-slide img-src="https://picsum.photos/1024/300/?image=23"></b-carousel-slide>

    </b-carousel>
    
    <div class="backgroud-bar">
      <h1>Categorias</h1> 
    </div>    

    <b-sidebar id="sidebar-right" title="Filtrar" right shadow no-header>
      <div class="p-3">

        <div class="d-flex justify-content-between">
          <h2>Filtrar</h2>
          <b-button variant="link" class="text-dark" v-b-toggle.sidebar-right><i class="fa fa-times"></i></b-button>
        </div>

        <b-form-group class="mb-3">
          <label>Nombre: </label>
          <b-form-input v-model="name" type="text" placeholder="Palabra clave de la categoria"></b-form-input>
        </b-form-group>

        <b-row>
          <b-button variant="dark" @click="getCategories()"><i class="fa fa-search"></i> Filtrar</b-button>
          <b-button id="limpiar" @click="cleanFilters()" class="mt-2"><i class="fa fa-broom"></i> Limpiar</b-button>
        </b-row>

      </div>    
    </b-sidebar>

    <div id="fondoItems">
      <b-overlay :show="loading" rounded="sm" variant="transparent" spinner-variant="white">
        <b-container>

          <b-row>
            <b-col cols="12" class="justify-content-end d-flex mt-3"><b-button v-b-toggle.sidebar-right><i class="fa fa-search"></i> Filtrar</b-button></b-col>
          </b-row> 

          <b-row>
              
              <b-col lg="3" sm="6" cols="12" v-for="category in categories" :key="category.id" class="mt-3 mb-2">
                <CategoryCard :category="category"/>  
              </b-col>
            
          </b-row>

        </b-container>
      </b-overlay>
    </div>

  </div>
</template>

<script>
import CategoryCard from "@/components/CategoryCard"

export default {
    name: 'Home',
    components: {
      CategoryCard
    },
    data() {
      return {
          slide: 0,
          sliding: null,
          categories: [],
          loading: true,
          name: '',     
      }   
    },
    mounted() {
      this.getCategories()
    },
    methods: {
      getCategories(){
          this.loading= true;
          let url = 'https://giannfrancoo-servicio-web.herokuapp.com/categorias?'

          fetch(url + new URLSearchParams({
            name: this.name,
          }))  
          .then(res => {
              return res.json()
          })
          .then(data => {
              this.categories = data;               
              this.loading = false;
          }) 
          .catch(e => {
            console.log(e.message)
          })
      },
      cleanFilters(){
        this.name = ''
        this.getCategories()
      },
      onSlideStart(){
        this.sliding = true
      },
      onSlideEnd(){
        this.sliding = false
      }

    },
  }
</script>


<style scoped>

  #fondoItems .container{
    min-height: 200px;
  }  

  #limpiar{
    background-color: rgb(255, 99, 71);
    border: none;
  }
  
</style>