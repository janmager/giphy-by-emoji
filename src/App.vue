<template>
  <div class="app">
    <div :class="[{ flexStart : step === 1 }, 'wrapper']">
      <transition name="slide">
        <img src="./assets/logo.png" class="logo" v-if="step === 1">
      </transition>
      <transition name="fade">
        <Background v-if="step === 0" />
      </transition>
      <Claim v-if="step === 0" />
      <div class="searchingRightNow">
        Searching right now: {{ searchEmoji }}
      </div>
      <SearchInput 
        v-model="searchValue"
        @input="handleEmoji"
        :dark="step === 1"
        id="search"
      />
      <button
        @click="handleInput">Search by Emoji</button>
      <div class="results" v-if="results && step === 1">
        <Item 
          v-for="item in results" 
          :item="item" 
          @click.native="handleModalOpen(item)"
          :key="item.id"/>
      </div>
      <Modal 
        v-if="modalOpen"
        @closeModal="modalOpen = false"
        :item="modalItem" />
      <Backdrop v-if="modalOpen" />
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import jquery from 'jquery';
  import emojidex from 'emojis-list';
  import debounce from 'lodash.debounce';
  import Claim from '@/components/Claim.vue';
  import SearchInput from '@/components/SearchInput.vue';
  import Background from '@/components/Background.vue';
  import Item from '@/components/Item.vue';
  import Modal from '@/components/Modal.vue';
  import Backdrop from '@/components/Backdrop.vue';

  global.jQuery = require('jquery');
  var $ = global.jQuery;
  window.$ = $;

  const API = 'http://api.giphy.com/v1/gifs/search?api_key=DEp6QvwCLGPbx3A8tqtBymRpVtcLG7OJ&limit=100&';
  const APIEmoji = 'https://www.emojidex.com/api/v1/emoji/';

  export default {
    name: 'App',
    components: {
      Claim,
      SearchInput,
      Background,
      Item,
      Modal,
      Backdrop
    },
    data(){
      return{
        modalItem: null,
        modalOpen: false,
        step: 0,
        searchValue: '',
        searchEmoji: '',
        results: [],
      };
    },
    methods: {
      handleEmoji: debounce(function(){
        axios.get(`${APIEmoji}${this.searchValue}`)
          .then((response) => {
            console.log(`${APIEmoji}${this.searchValue}`);
            // console.log(response.data.moji);
            if(response.data.moji != undefined){
              this.searchEmoji += response.data.moji + ' ';
              $("#search").val('');
              console.log(this.searchEmoji);
            }
          })
          .catch((error) => {
            console.log(error);
          });
      }, 500),
      handleModalOpen(item){
        this.modalOpen = true;
        this.modalItem = item;
      },
      handleInput(){
        axios.get(`${API}q=${this.searchValue}`)
          .then((response) => {
            console.log(`${API}q=${this.searchValue}`);
            this.results = response.data.data;
            this.step = 1;
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  };
</script>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css?family=Montserrat:100,100i,200,200i,300,300i,400,400i,500,500i,600,600i,700,700i,800,800i,900,900i');
  @import url('https://meyerweb.com/eric/tools/css/reset/reset.css');

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  body{
    font-family: Montserrat, sans-serif;
    margin: 0;
    padding: 0;
  }
  .searchingRightNow{
    background: red;
    color: yellow;
    padding: 20px;
    font-size: 20px;
    font-weight: 800;
    border: 3px solid yellow;
    margin-top: 50px;
  }
  button{
    margin-top: 30px;
    font-size: 20px;
  }
  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to{
    opacity: 0;
  }
  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
  }
  .slide-enter, .slide-leave-to{
    margin-top: -50px;
  }
  .wrapper{
    display: flex;
    position: relative;
    flex-direction: column;
    align-items: center;
    box-sizing: border-box;
    padding: 30px;
    margin: 0;
    min-width: 100%;
    min-height: 100vh;
    font-family: Montserrat, sans-serif;
    text-align: center;
    justify-content: center;
    align-items: center;

    &.flexStart{
      justify-content: flex-start;
    }
  }
  .logo{
    position: absolute;
    top: 30px;
    max-height: 20px;
  }
  .results{
    width: 95%;
    margin-top: 50px;
    max-width: 1250px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 20px;
    align-items: center;
    justify-items: center;

    @media(max-width: 1250px){
      grid-template-columns: 1fr 1fr 1fr;
    }

    @media(max-width: 850px){
      grid-template-columns: 1fr 1fr;
    }

    @media(max-width: 500px){
      grid-template-columns: 1fr;
    }
  }
  .lds-dual-ring {
  display: inline-block;
  width: 64px;
  height: 64px;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 46px;
  height: 46px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #fff;
  border-color: #fff transparent #fff transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}


</style>
