<template>
    <div class="container animated bounce" v-if="detailsOfPlayer.real_name !== ''">
        <div id="detailsCard" class="card bg-dark">
            <div class="card-body">
                <h5 class="changeTrans1 card-title">{{ detailsOfPlayer.real_name }}</h5>
                <h6 class="changeTrans1 card-subtitle mb-2">{{ detailsOfPlayer.player_name }}</h6>
                <h6 class="changeTrans1 card-subtitle mb-2">{{ detailsOfPlayer.asset }}</h6>
                <button id="sendDataBtn" class="changeTrans1 btn btn-success rounded-0 text-uppercase disabled" v-on:click="sendDataToBE">send</button>
            </div>
        </div>
    </div>
</template>

<script>

    import axios from 'axios';
    export default {
        name: "Details",
        props: {
            detailsOfPlayer: {}
        },
        data: function() {
            return {
                player: []
            };
        },
        methods: {
            async sendDataToBE() {
                if (this.detailsOfPlayer.real_name !== undefined) {
                    try {
                        axios({
                            method: 'post',
                            url: 'http://mockbin.com/request?',
                            data: {
                                real_name: this.detailsOfPlayer.real_name,
                                player_name: this.detailsOfPlayer.player_name,
                                asset: this.detailsOfPlayer.asset
                            },
                            headers: {
                                'Content-Type': 'application/json'
                            }
                            // eslint-disable-next-line no-unused-vars
                        }).then(function (response) {

                        });
                    } catch (error) {
                        // eslint-disable-next-line no-console
                        console.log(error)
                    }
                }
            }
        }
    }

</script>

<style scoped>

    #detailsCard{
        position: sticky;
        top: 0;
    }

    @font-face {
        font-family: "CODE";
        src: url("../assets/font/CODE Bold.otf");
    }

    .card{
        transition: opacity 0.5s ease-in-out;
        font-family: 'CODE', Arial, sans-serif;
        color: white;
        border-radius: 0;
        -webkit-box-shadow: 10px 10px 25px 2px rgba(128,128,128,1);
        -moz-box-shadow: 10px 10px 25px 2px rgba(128,128,128,1);
        box-shadow: 10px 10px 25px 2px rgba(128,128,128,1);
    }

    .card-subtitle{
        color: #818d96;
    }

    .changeTrans1{
        opacity: 0;
        transition: all 0.5s ease;
    }

</style>