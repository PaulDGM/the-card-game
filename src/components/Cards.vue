<template>
      <div class="container" v-if="loading">
        <div class="row">
          <div v-for="(player, index) in sortedPlayers" v-bind:key="player.real_name" class="col-sm-4">
            <div v-on:click="sendData(index, player.real_name, player.player_name, player.asset)" class="clickme pt-5 card">

              <div class="img-box mr-auto ml-auto text-center mb-4">
                <img src="../assets/card_images/cardimg.png" alt="card image" class="w-50 round-img"/>
              </div>

              <div class="card-title">
                <h3 class="changeTrans text-truncate">{{ player.real_name }}</h3>
              </div>
              <div class="changeTrans card-subtitle text-truncate">{{ player.player_name }}</div>
              <div class="changeTrans card-subtitle text-truncate">{{ player.asset }}</div>
            </div>
          </div>
        </div>
      </div>
  <div v-else class="container-fluid text-center">
    <div class="spinner-grow text-dark" role="status">
      <span class="sr-only">Loading...</span>
    </div>
  </div>
</template>

<script>

  import axios from 'axios';

  export default{
    name: 'Cards',
    props: {
      sort: {}
    },
    data(){
      return{
        loading: false,
        players: '',
        sortKey: 'real_name'
      }
    },
    created(){
      this.data();
    },
    methods: {
      async data(){
        var vue = this;
        const ax = axios.create({
          baseURL: window.location.href
        });
        await ax.get('/players.json')
                .then(function (response) {
                  vue.players = response.data;
                  vue.loading = true;
                })
                .catch(function (error) {
                  // eslint-disable-next-line no-console
                  console.log(error);
                })
                .then(function () {
                });
      },
      sendData: function(index, realName, playerName, asset){
        var cards = document.getElementsByClassName("card");
        for(var i = 0; i < cards.length; i++){
          cards[i].style = "opacity: 0.5; background-color: #a9a9a9;";
        }
        cards[index+1].style= "opacity: 1; background-color: #343a40;";

        let newPlayer = {
          real_name: realName,
          player_name: playerName,
          asset: asset
        };

        this.$emit("detailedPlayerInfo", newPlayer);
      }
    },
    computed: {
      sortedPlayers: function() {

          var array = this.players;
          var key = this.sortKey;

        if(this.sort === 'asc') {
          var ascSorted = array.sort(function (a, b) {
            var x = a[key];
            var y = b[key];
            return ((x < y) ? -1 : ((x > y) ? 1 : 0));
          });
          return ascSorted;
        }
        else if(this.sort === 'desc'){
          var descSorted =  array.sort(function (a, b) {
            var x = a[key];
            var y = b[key];
            return ((x > y) ? -1 : ((x < y) ? 1 : 0))
          });
          return descSorted;
        }
        else{
          return this.players;
        }
      }
    }
  }

</script>

<style scoped>

  @font-face {
    font-family: "CODE";
    src: url("../assets/font/CODE Bold.otf");
  }

  .card{
    font-family: 'CODE', Arial, sans-serif;
    -webkit-box-shadow: 10px 10px 25px 2px rgba(128,128,128,1);
    -moz-box-shadow: 10px 10px 25px 2px rgba(128,128,128,1);
    box-shadow: 10px 10px 25px 2px rgba(128,128,128,1);
    margin-top: 80px;
    background-color: #a9a9a9;
    opacity: 0.5;
    color: white;
    padding: 20px;
    border-radius: 0;
    transition: all 0.3s ease;
  }

  .card:hover{
    opacity: 1;
    -webkit-transform: scale(1.1);
    -ms-transform: scale(1.1);
    transform: scale(1.1);
    background-color: #343a40;
  }

  .card-subtitle{
    color: #def3ff;
  }

  .round-img{
    border-radius: 50%;
    border: solid 3px white;
    /*-webkit-box-shadow: 6.5px 6.5px 5px 0px rgba(110,107,110,1);
    -moz-box-shadow: 6.5px 6.5px 5px 0px rgba(110,107,110,1);
    box-shadow: 6.5px 6.5px 5px 0px rgba(110,107,110,1);*/
  }

  .img-box{
    margin-top: -105px;
  }

  .changeTrans{
    transition: all 0.5s ease;
  }

</style>
