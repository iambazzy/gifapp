<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class App extends Vue {
  
mounted() {
  const cdn1 = document.createElement('link');
  cdn1.setAttribute('rel', 'stylesheet');
  cdn1.setAttribute('href', 'https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css');
  document.head.appendChild(cdn1);

  const cdn2 = document.createElement('script');
  cdn2.setAttribute('src', 'https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js');
  document.head.appendChild(cdn2);
 
  const cdn3 = document.createElement('script');
  cdn3.setAttribute('src', 'https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js');
  document.head.appendChild(cdn3);

  const cdn4 = document.createElement('link');
  cdn4.setAttribute('rel', 'stylesheet');
  cdn4.setAttribute('href', 'https://cdn.jsdelivr.net/npm/uikit@3.5.4/dist/css/uikit.min.css');  
  document.head.appendChild(cdn4);

  const cdn5 = document.createElement('script');
  cdn5.setAttribute('src', 'https://cdn.jsdelivr.net/npm/uikit@3.5.4/dist/js/uikit.min.js');
  document.head.appendChild(cdn5);

  const cdn6 = document.createElement('script');
  cdn6.setAttribute('src', 'https://cdn.jsdelivr.net/npm/uikit@3.5.4/dist/js/uikit-icons.min.js');
  document.head.appendChild(cdn6);

  const cdn7 = document.createElement('link');
  cdn7.setAttribute('rel', 'stylesheet');
  cdn7.setAttribute('href', "https://fonts.googleapis.com/css2?family=Bangers&display=swap");
  document.head.appendChild(cdn7);
}
}
</script>

<style lang="scss">

</style>

