<template>
  <div class="home">
    <div class="container mt-5">
      <ul class="list-group">
        <li class="list-group-item" v-for="(data, index) in news" v-bind:key="index">
          Date :{{ data.date_et_heure }} <br>
          Type: {{  data.type }}<br>
          Titre {{  data.titre }}<br>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import axios from 'axios';
import { defineComponent } from 'vue';

type News = {
  type: string;
  titre: string;
  date_et_heure: string;
}

export default defineComponent({
  name: 'HomeView',
  data(){
    return {
      news:[] as News[],
      length:1
    }
  },
  mounted() {
    setInterval(() => {
      axios.get('http://localhost:3000/news/'+this.length)
      .then((response) => {
        response.data.length > 0 && this.news.push(response.data)
       this.length++    
      })
}, 1000);

      
  },
});
</script>
