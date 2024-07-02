<template>
    <div v-if="listerwala.length" class="griddesh" style="margin-top: 100px;">
            <div v-for="anime in listerwala">
                <Thumbnail 
                    :image= anime.imagesh
                    :title = anime.titlesh 
                    :plus = false />
            </div>
    </div>
    <div v-else >
        <div style="font-size: 80px; display: flex; justify-content: center; color:rgb(199, 198, 198); margin-top: 50px;">
            Your Watchlist is Empty &#128531;
        </div>
        
        <div style="font-size: 20px; display: flex; justify-content: center; color:rgb(199, 198, 198);">
            <a href="../index.html">Click this link to add soemthing to your watchlist </a>
        </div>"
    </div>
    
    
</template>

<script>
    import Thumbnail from './Thumbnail.vue'
    export default{
        components:{
            Thumbnail
        },
        methods:{
              
        },
        data(){
            return{
                listerwala:JSON.parse(localStorage.getItem('Watchlist'))
            }
        }
    }
</script>

<style>
    .btn{
        background-color: rgba(26, 6, 6, 0.918);
    }

    .griddesh{
        display: grid;
        grid-template-columns:1fr 1fr 1fr 1fr;
    }
    .former{
        margin-top: 100px;
    }
</style>