<template>
            
    <b-card
        :title="category.name"        
        :img-src="getImagen(category.image)" 
        img-alt="Imagen" 
        img-top
        class="text-center h-100"
    >     
        <hr class="my-1">

        <b-button pill :to="'categorias/' + category.id + '/items/' + category.name" variant="dark" block class="w-100 mt-2"><i class="fa fa-search"></i> Ver items</b-button>
    </b-card>
    
</template>

<script>
import default_image from "@/assets/default_image.jpg"
export default {
    name: "CategoryCard",
    props: [
        "category"
    ],
    methods: {      
        getImagen(img){
            if(img != null){
                return img
            }
            else{
                return default_image
            }          
        }
    }     
}
</script>

<style lang="scss">
    .card{
        border-style: none;

        &:hover {
            box-shadow: 0px 0px 5px white;
        }

        .card img:hover{
            transition: opacity 0.3s;
            opacity: 0.7;
        }

        .card-img-top {
            width: 100%;
            height: 12rem;
            object-fit: cover;
        }
    }
</style>