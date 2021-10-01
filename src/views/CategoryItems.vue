<template>
  <div id="fondoCards" class="CategoryItem">

    <div class="backgroud-bar">
      <h1>{{ category_name }}</h1> 
    </div>

    <b-sidebar id="sidebar-right" title="Filtrar" right shadow no-header>
      <div class="p-3">

        <div class="d-flex justify-content-between">
          <h2>Filtrar</h2>
          <b-button variant="link" class="text-dark" v-b-toggle.sidebar-right><i class="fa fa-times"></i></b-button>
        </div>

        <b-form-group class="mb-3">
          <label>Nombre: </label>
          <b-form-input v-model="name" type="text" placeholder="Palabra clave del item"></b-form-input>
        </b-form-group>

        <b-form-group class="mb-3">
          <label>Precio máximo: ${{ maxPrice }}</label>
          <b-form-input class="w-100" v-model="maxPrice" type="range" min="0" max="4000"></b-form-input>
        </b-form-group> 

        <b-row>
          <b-button variant="dark" @click="getItems()"><i class="fa fa-search"></i> Filtrar</b-button>
          <b-button id="limpiar" @click="cleanFilters()" class="mt-2"><i class="fa fa-broom"></i> Limpiar</b-button>
        </b-row>

      </div>    
    </b-sidebar>

    <b-overlay :show="loading" rounded="sm" variant="transparent" spinner-variant="white">
      <b-container>      
        <b-row>    
          <b-col cols="12" class="justify-content-end d-flex mt-3"><b-button v-b-toggle.sidebar-right>Filtrar</b-button></b-col>
        </b-row>
        <b-row>
          
            <b-col lg="3" sm="6" cols="12" v-for="item in items" :key="item.id" class="mt-3 mb-2">
                <ItemCard :item="item"/>
            </b-col> 

        </b-row>      
      </b-container>
    </b-overlay>

  </div>
</template>

<script>
import ItemCard from "@/components/ItemCard"

export default {
    name: 'CategoryItem',
    components: {
      ItemCard
    },
    data() {
      return {
        category_id: 0,
        category_name: '',
        maxPrice: 0,
        name: '',
        items: [],  
        loading: true,  
      }   
    },
    mounted() {
      this.category_id = this.$route.params.id
      this.category_name = this.$route.params.category_name
      this.getItems()
    },
    methods: {
      getItems(){
        this.loading = true;
        let url = "https://giannfrancoo-servicio-web.herokuapp.com/categorias/" + this.category_id + "/items?"

        fetch(url + new URLSearchParams({            
            maxPrice: this.maxPrice == 0 ? '' :this.maxPrice,
            name: this.name
        }))   
        .then(res => {
            return res.json()
        })
        .then(data => {
            this.items = data;
            this.loading = false;
        }) 
        .catch(e => {
            console.log(e.message)
        })
      },

      cleanFilters(){
        this.maxPrice = 0
        this.name= ''
        this.getItems()
      }
    }
  }
  
</script>

<style scoped>

  #range-id{
    color:white;
  }

  #limpiar{
    background-color: rgb(255, 99, 71);
    border: none;
  }

</style>