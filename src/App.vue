<template>
  <div id="app">
    <div class="image-header">
      <img alt="Stroyblok logo" src="./assets/logo.png" />
    </div>
    <Select v-on:update-filter="sendFilter" v-on:update-type="sendType" />
    <Loading v-if="!contentRepositories" />
    <ListOfRepositories
      :json-data="contentRepositories"
      :filter="filterId"
      :type="typeId"
      v-on:show-repos="changeLoading"
    />
  </div>
</template>

<script>
import Select from './components/Select.vue';
import Loading from './components/Loading.vue';
import dataFromJson from '../scripts/crawler-repositories/data/repositories.json'
import ListOfRepositories from './components/ListOfRepositories.vue';

export default {
  name: 'App',
  components: {
    Select,
    Loading,
    ListOfRepositories,
  },

  data() {
    return {
      contentRepositories: dataFromJson,
      filterId: '',
      typeId: '',
      isLoading: true,
    };
  },

  methods: {
    sendFilter(val) {
      this.filterId = val;
    },

    sendType(val) {
      this.typeId = val;
    },

    changeLoading(val) {
      this.isLoading = val;
    },
    // async loadFiles () {
    //   return await loadRepositoriesJson()
    //   // console.log(content)
    // }
  },
};
</script>

<style>
#app {
  margin: 0 auto;
  width: 80%;
}

#app img {
  margin-top: 20px;
  width: 50%;
  justify-content: center;
}

.image-header {
  display: flex;
  justify-content: center;
}

@media only screen and (max-width: 425px) {
  #app {
    width: 90%;
  }
}
</style>
