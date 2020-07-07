<template>
  <div class="container"> 
      <div class="row">
        <div class="col-lg-12 head text-center">Gif Search Engine</div>
      </div>
      <div class="row">
        <div class="col-lg-12 search-div text-center">
          <div class="uk-inline">
            <span class="uk-form-icon" uk-icon="icon: search"></span>
            <input class="uk-input search-bar" v-model="searchVal" required>
          </div>
          <button class="uk-button uk-button-default custom-button" @click="searchGif()">Search</button>
        </div>
      </div>
      <div v-if="loading === true" class="loading-class" uk-spinner="ratio: 3"></div>
      <div v-else>
        <div class="row gif-container">
          <div class="col-lg-3 col-md-3 col-sm-4 col-xs-6 col gif-card" v-for="(gif, index) in gifs" :key="index"> 
             <img class="my-image" :src="gif.realUrl" height="100%" width="100%"  />
          </div>  
        </div>
      </div>
  </div>
</template>

<script lang="tsx">
import { Component, Prop, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class HelloWorld extends Vue {

  gifs: any = [];
  loading = true;
  searchVal = '';

  mounted() {
    this.getData();
  }

  searchGif() {
    if(this.searchVal !== '') {
      this.loading = true;
      axios.get(`https://api.giphy.com/v1/gifs/search?api_key=abG2UewkaFdc33MLZ0JcAe48WbopEDIy&q=${this.searchVal}&limit=25&offset=0&rating=g&lang=en`)
      .then((resp) => {
        if (this.gifs.length > 0) {
          this.gifs = [];
          const { data : { data } } = resp;
          data.forEach((el: any) => {
            const dataObj = {
            ...el,
            realUrl: `https://media.giphy.com/media/${el.id}/giphy.gif`
            }
          this.gifs.push(dataObj);
          })
         this.loading = false;
        }
      })
      .catch((err)=> {
        console.log(err)
      })
    }
  }

  getData() {
    axios.get('https://api.giphy.com/v1/gifs/trending?api_key=abG2UewkaFdc33MLZ0JcAe48WbopEDIy&limit=25&rating=g')
    .then((resp) => {
      this.loading = false;
      const { data : { data } } = resp;
      data.forEach((el : any) => {
        const dataObj = {
          ...el,
          realUrl: `https://media.giphy.com/media/${el.id}/giphy.gif`
        }
        this.gifs.push(dataObj);
      });
    })
    .catch((err) => {
      console.log(err)
    })
  }


}
</script>

<style scoped lang="scss">
* {
  box-sizing: border-box;
}
.hey {
  background-color: red;
  height: 300px;
}
.head {
  height: 100px;
  padding: 1%;
  background-color: black;
  font-family: 'Bangers', cursive;
  font-size: 40px;
  color: white;
  letter-spacing: 2px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 3px 5px -3px black;
}
.gif-container {
  box-sizing: border-box;
  padding: 0% 3%;
  margin-top: 5%;
}
.gif-card {
  height: 160px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1%;
}
.my-image {
  height: 100%;
  width: 100%;
  border-radius: 2px;
}
.search-div {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-top: 2%
}
.search-bar {
  width: 400px;
  border: 1px solid gray;
  border-radius: 5px;
  font-family: 'Bangers';
  letter-spacing: 1px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.custom-button {
  background-color: black;
  border-radius: 5px;
  color: white;
  font-family: 'Bangers', cursive;
  font-size: 20px;
  letter-spacing: 1.5px;
}
.loading-class {
  display: flex;
  height: 500px;
  justify-content: center;
  align-items: center;
}

@media only screen and (max-width: 420px) {
 .gif-card {
    height: 160px;
 }
 .search-div {
   display: flex;
   justify-content: space-between;
   padding: 0% 6%;
 }
 .search-bar {
   width: 250px;
 }
 .custom-button {
   width: 100px;
   display: flex;
   justify-content: center;
 }
}

@media only screen and (max-width: 380px) {
 .search-bar {
   width: 180px;
 }
 .custom-button {
   width: 100px;
   display: flex;
   justify-content: center;
 }
}
</style>
