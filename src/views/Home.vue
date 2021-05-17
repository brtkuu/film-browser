<template>
  <div class="wrapper">
  <transition name="fade">
  <Cinema v-if="step === 0"/>
  </transition>
    <Input @searchClick="handleSearch" :step='step'/>
    <Loading v-if="loading" />
    <div class="itemWrapper">
    <Info v-for="item in results" :key="item.id" :item="item" @showInfo="dispInfo(item)"/>
    <Modal v-if="info" :modalInfo="modalInfo" @closeButton="closeInfo"/>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2';
import axios from 'axios';
import Input from '../components/Input.vue';
import Cinema from '../components/Cinema.vue';
import Info from '../components/Info.vue';
import Loading from '../components/Loading.vue';
import Modal from '../components/Modal.vue';

const api = 'https://api.themoviedb.org/3/search/movie?api_key=0380482adf86754e90be0cfcf0a2ed1b';

export default {
  name: 'home',
  components: {
    Input, Cinema, Info, Loading, Modal,
  },
  data() {
    return {
      searchValue: '',
      step: 0,
      results: [],
      loading: false,
      info: false,
      modalInfo: null,
    };
  },
  methods: {
    async handleSearch(searchValue) {
      if (searchValue !== '') {
        this.loading = true;
        this.step = 1;
        await axios.get(`${api}&query=${searchValue}`).then((response) => { this.results = response.data.results; });
        this.results.sort((a, b) => ((a.vote_average > b.vote_average) ? -1 : 1));
        this.loading = false;
      } else {
        Swal.fire({
          icon: 'warning',
          title: 'Warning!',
          text: 'No argument',
        });
      }
    },
    dispInfo(item) {
      this.modalInfo = item;
      this.info = true;
    },
    closeInfo() {
      this.modalInfo = null;
      this.info = false;
    },
  },

};

</script>
<style lang="scss" scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity .2s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
  .wrapper{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    // align-items: center;
  }
  .itemWrapper{
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 20px;
  }
</style>
