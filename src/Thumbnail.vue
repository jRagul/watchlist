<template>
    <div class="container" >
            <div class="row">
                <div class="col s12 m20">
                    <div class="card">
                        <div class="card-image">
                            <img :src="image">
                            <a v-if="plus" class="btn-floating halfway-fab waves-effect waves-green deep-purple lighten-5 modal-trigger" data-target="modalesh" @click="store()" ><i class="material-icons black-text">add</i></a>
                            <a v-else class="btn-floating halfway-fab waves-effect waves-teal deep-purple lighten-5" @click="remove()"><i class="material-icons black-text">remove</i></a>
                        </div>
                        <div class="card-content white-text">
                            {{ title }}
                        </div>
                    </div>
                </div>
            </div>
            
    </div>
    <div id="modal1" class="modal container">
        <div style="display:flex; justify-content:center; padding-left: 0px; padding-right: 0px;" class="modal-content container" >
            <p id="that" style="font-size: 30px;">Added to Watchlist!</p>
        </div>
        
  </div>

  <a style="display:none" id="zemn" class="btn modal-trigger" data-target="modal1">dasdas</a>
    
    
    
</template>


<script>
    
    //https://imdbapi.dev/ integrate this next time you open
    export default{
        props:{
            image:{
                type:String
            },
            title:{
                type:String
            },
            plus:{
                type:Boolean
            }
        },
        mounted(){
            const elems = document.querySelectorAll('.modal');
            M.Modal.init(elems,{
                startingTop:"10%",
                endingTop:"30%"
            });
        },  
        methods:{
            modale(){
                if(this.modalflag){
                    return 'modal1'
                }
                else{
                    return 'modal2'
                }
            },
            update(){
                this.localWatchlist = this.getWatchlist()
            },
            remove(){
                let watchlist = this.getWatchlist()
                let indexToRemove = watchlist.findIndex(anime => anime.titlesh === this.title);
                if (indexToRemove !== -1) {
                    watchlist.splice(indexToRemove, 1);
                    localStorage.setItem('Watchlist', JSON.stringify(watchlist));
                    this.update();
                    location.reload()
                }
            },
            getWatchlist(){
                let watchlist = localStorage.getItem('Watchlist');
                return watchlist ? JSON.parse(watchlist) : [];
            },
            check(title){
                let watchlist = this.getWatchlist()
                if(watchlist.some(anime => anime.titlesh == title.titlesh)){
                    
                    return true;
                }
            },
            store(){   // function to store the shows in the watchlist key in localstorage
                const storesh = {
                    titlesh : this.title,
                    imagesh : this.image
                }
                if(localStorage.getItem("Watchlist")){
                    if( this.check(storesh)){
                        //alert("Already in Watchlist")
                        document.getElementById('that').innerHTML = "Already in Watchlist"
                        document.getElementById('zemn').click()
                        return
                    }
                    document.getElementById('that').innerHTML = "Added to Watchlist"
                    document.getElementById('zemn').click()
                    let gettesh = JSON.parse(localStorage.getItem("Watchlist"))
                    gettesh.push(storesh)
                    localStorage.setItem('Watchlist', JSON.stringify(gettesh))
                    this.update()
                }
                else{
                    document.getElementById('that').innerHTML = "Added to Watchlist"
                    document.getElementById('zemn').click()
                    let jsonarray = [storesh]
                    localStorage.setItem('Watchlist', JSON.stringify(jsonarray))
                    alert("Added to Watchlist!!")
                    this.update()
                }

            }
        },
        data(){
            return{
                buton:false,
                index:0,
                localWatchlist: this.getWatchlist()
            }
        }
    }
</script>

<style>
    .card .card-content{
        padding-left: 10px;
        padding-right: 5px;
    }
    .disable{
        pointer-events:none
    }
    .buton{
        pointer-events: none;
    }
    .card{
        background-color:#161c1c;
    }
    .card-image img {
        width: 100%;
        height: auto;
        object-fit: cover;
        border-radius: 20px; 
    }
    .name{
        text-align: center;
        background-color: rgb(30, 78, 85);
        width:225px;
        border-radius: 18px;
        padding: 5px
    }
</style>

