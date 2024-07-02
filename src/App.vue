<template>
    <div>
        <div class="container">
        <div class="former">
            <form @submit.prevent="submitForm" class="container">
            <div class="row" style="margin-top: 20px;">
                <div class="col l10"><input v-model=searchTerm type="text" placeholder="Search" class="white-text" style="padding-left: 20px"></div>
                <div class="col l2"><a style="margin-left:20px; margin-top:10px" class="btn" @click.prevent="submitForm"><i class="material-icons left" style="margin-right:0px">search</i></a></div>
            </div>
            <label>
                <input id="checkesh" type="checkbox" class="filled-in" />
                <span>Manga</span>
            </label>
        </form>
        </div>
        </div>
    </div>
    
    <div class="griddesh">
        <div v-for="anime in info.data">
                <Thumbnail 
                    :image= anime.images.webp.image_url
                    :title = anime.title 
                    :plus = true />
        </div>
    </div>
    
</template>


<script>
    
    import Thumbnail from './Thumbnail.vue'
    import axios from 'axios'
    import {ref} from 'vue'


    export default{
        components:{
            Thumbnail
        },
        setup(){
            const info = ref('')
            const searchTerm = ref('')
            axios.get(`https://api.jikan.moe/v4/anime?q=${searchTerm.value}&sfw=true`)
                    .then(response =>{
                    console.log(searchTerm.value)
                    info.value = response.data
                    console.log(info.value)
            })
            const submitForm = () =>{
                const checkesh = document.getElementById("checkesh") // gets checkbox value
                console.log(checkesh.checked)
                if(checkesh.checked){ // calls manga if check box is checked
                    axios.get(`https://api.jikan.moe/v4/manga?q=${searchTerm.value}&sfw=true`)
                    .then(response =>{
                    console.log(searchTerm.value)
                    info.value = response.data
                    console.log(info.value)
                })
                }
                else{ //calls anime api if checkbox is checked
                    axios.get(`https://api.jikan.moe/v4/anime?q=${searchTerm.value}&sfw=true`)
                    .then(response =>{
                    console.log(searchTerm.value)
                    info.value = response.data
                    console.log(info.value)
                })
            }

            }
            
            return{
                info,
                searchTerm,
                submitForm
            }
        },
        methods:{
        },
        data(){
            return{
            }
            
        }
    }
</script>

<style>
    .mainDiv{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
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