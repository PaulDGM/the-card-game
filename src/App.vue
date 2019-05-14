<template>
  <div id="app">
    <div class="sticky-top row container ml-auto mr-auto mb-5 mt-5 pr-4">
      <Details class="col" :detailsOfPlayer="playerDetailsData"/>
      <Controls class="justify-content-center align-items-center col-sm-3" @sort="sort"/>
    </div>
    <div class="container">
      <Cards @detailedPlayerInfo="updateMessage" :sort="sortWay"/>
    </div>
  </div>
</template>

<script>

import Cards from './components/Cards.vue'
import Details from './components/Details.vue'
import Controls from './components/Controls.vue'

export default {
  name: 'app',
  components: {
    Cards,
    Details,
    Controls
  },
  data: function() {
    return {
      playerDetailsData: "",
      sortWay: ""
    };
  },
  methods: {
    setData(data) {
      this.playerDetailsData = data;
    },
    //gets details from the player-cards and changes style and sets Data to/of the detail view
    updateMessage(details) {
      // eslint-disable-next-line no-undef
      $("#sendDataBtn").removeClass("disabled");
      // eslint-disable-next-line no-undef
      $(".changeTrans1").css({'opacity': '0'});
      var vue = this;
      setTimeout(
              function () {
                // eslint-disable-next-line no-console
                console.log(details)
                vue.setData(details);
                // eslint-disable-next-line no-undef
                $(".changeTrans1").css({'opacity': '1'});
              }, 300);
      // eslint-disable-next-line no-undef
      $("#detailsCard").css({
        'visibility': 'visible',
        'opacity': '1'
      });

      // eslint-disable-next-line no-undef
      if ($("#detailsCard").offsetHeight < 100) {
        // eslint-disable-next-line no-undef
        $("#detailsCard").slideToggle("slow", function () {

        });
      }
    },
    sortData(data){
      this.sortWay = data;
    },
    //gets the way to sort the data after clicking the button "SORTIEREN" and runs sortData and changes opacity after 0.3s
    sort(sortWay) {
      // eslint-disable-next-line no-undef
      $(".changeTrans").css({'opacity': '0'});
      var vue = this;
      setTimeout(
              function () {
                vue.sortData(sortWay)
                // eslint-disable-next-line no-undef
                $(".changeTrans").css({'opacity': '1'});
              }, 300);
    },
  }
}

</script>

<style>

body {
  background: #D3CCE3;
  background: -webkit-linear-gradient(to right, rgba(240, 190, 213, 0.47), rgba(0, 0, 0, 0.2));
  background: linear-gradient(to right, rgba(240, 190, 213, 0.47), rgba(0, 0, 0, 0.2));
}

</style>