<template>
  <div id="app">
    <h1>{{title}}</h1>
    <form @submit.prevent="formSubmitted()">
            <label for="searchTerm">Search Term</label>
            <input
              v-model="searchTerm"
              class="u-full-width"
              type="text"
              id="searchTerm"
              name="searchTerm" />
            <button type="submit">Search</button> <br/>
    </form>
    <img v-if="loading" class="loading" src="https://i.imgur.com/RlS6YST.gif"/>
    <section class="images">
      <img v-for="image in images" :key="image.id" :src="image.urls.small">
    </section>
  </div>
</template>

<script>
import API from './API';

export default {
  name: 'app',
  data() {
    return {
      title: 'Vue.JS Image Search App',
      searchTerm: '',
      images: [],
      loading: false
    };
  },
  methods: {
    formSubmitted() {
      this.loading = true;
      this.images = [];
      API.search(this.searchTerm)
        .then(images => {
          this.images = images;
          this.loading = false;
        });
    }
  },
};
</script>

<style>
body {
  width: 80%;
  margin: 2em auto 0 auto;
}

.images {
  column-count: 3;
}

.loading {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 5%;
}

img {
  width: 100%;
}
</style>
