<template>
    <div class="d-inline-flex pr-auto pl-auto">
        <div class="row">
            <button v-on:click="submitASC()" class="btn col sorting rounded-0" id="asc">
                <img src="../assets/asc.png" width="20" height="20" alt="sort AZ">
            </button>
            <button v-on:click="submitDESC()" class="btn col sorting rounded-0" id="desc">
                <img src="../assets/desc.png" width="20" height="20" alt="sort ZA">
            </button>
            <button v-on:click="submit()" class="w-100 btn btn-success rounded-0 text-uppercase">
                Sotieren
            </button>
        </div>
    </div>
</template>

<script>

    export default {
        name: "Controls",
        data() {
            return {
                sort: ""
            };
        }, methods: {
            submitASC: function () {
                this.sort = "asc";
                document.getElementById("asc").style = "background-color: darkgray;";
                document.getElementById("desc").style = "background-color: none;";

            },
            submitDESC: function () {
                this.sort = "desc";
                document.getElementById("asc").style = "background-color: none;";
                document.getElementById("desc").style = "background-color: darkgray;";
            },
            submit: function(){
                this.$emit("sort", this.sort);
                this.sort = "";
            }
        }
    }

</script>

<style scoped>

    @font-face {
        font-family: "CODE";
        src: url("../assets/font/CODE Bold.otf");
    }

    label{
        font-family: 'CODE', Arial, sans-serif;
        color: white;
    }

    .sorting:hover{
        background-color: #818d96;
    }

</style>