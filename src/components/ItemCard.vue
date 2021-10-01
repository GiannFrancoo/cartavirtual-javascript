<template>

    <b-card
        :title="item.name"
        :img-src="getImagen(item.image)"
        img-alt="Imagen"
        img-top
        class="h-100"
        >
        <hr class="my-1">
        <b-card-text>
            <p class="mt-2">{{ item.description }}</p>
        </b-card-text>
        <template #footer>
            <span>${{ item.price }}</span>
        </template>
    </b-card>

</template>

<script>

import default_image from "@/assets/default_image.jpg"

export default {
    name: "ItemCard",
    props: [
        "item"
    ],
    methods: {      
        getImagen(img){
            if(img != null){
                return img;
            }
            else{
                return default_image 
            }        
        },
    }     
}
</script>


<style lang="scss">
    .card {
        border-style: none;

        &:hover {
            box-shadow: 0px 0px 5px white;
        }

        .card-img-top {
            width: 100%;
            height: 12rem;
            object-fit: cover;
        }

        .card-footer {
            border-top: none;
            background: #FFF;
            color: #000;
            font-size: 1.25em;
            text-align: right;
        }
    }
</style>
