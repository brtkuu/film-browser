<template>
    <div class="modalWrapper">
        <loading v-show="!imdb && !genre && !production_countries" />
        <div v-show="imdb && genre && production_countries">
        <h1 class="modalTitle"> {{ modalInfo.title }} </h1>
        <p class="modalOverwiew"> {{ modalInfo.overview }}</p>
        <p class="modalOverwiew"> <b>Genre:</b> {{this.genre}} </p>
        <p class="modalOverwiew"> <b>Production countries:</b> {{this.production_countries}} </p>
        <p class="modalRating"> Rating: {{ modalInfo.vote_average }}</p>
        <p><a :href="imdb">IMDB link</a></p>
        </div>
        <div class="closeButton" v-on:click="$emit('closeButton')"></div>
    </div>
</template>
<script>
import axios from 'axios';
import Loading from './Loading.vue';

export default {
  components: { Loading },
  name: 'Modal',
  props: ['modalInfo'],
  data() {
    return {
      imdb: undefined,
      genre: undefined,
      production_countries: undefined,
    };
  },
  async mounted() {
    const ids = await axios.get(`https://api.themoviedb.org/3/movie/${this.modalInfo.id}/external_ids?api_key=0380482adf86754e90be0cfcf0a2ed1b`);
    this.imdb = `https://www.imdb.com/title/${ids.data.imdb_id}`;
    const details = await axios.get(`https://api.themoviedb.org/3/movie/${this.modalInfo.id}?api_key=0380482adf86754e90be0cfcf0a2ed1b&language=en-US`);
    this.genre = (details.data.genres.map(e => e.name).join(', ')).toLowerCase();
    this.production_countries = (details.data.production_countries.map(e => e.name).join(', '));
  },
};
</script>
<style lang="scss" scoped>
    .modalWrapper{
        position: fixed;
        top: 50%;
        left: 50%;
        height: auto;
        width: 50%;
        transform: translate(-50%, -50%);
        box-shadow: 0 0 8px 1px rgba($color: #1a1a1a, $alpha: 0.8);
        border: 2px solid black;
        background: white;
        padding: 10px;
        @media (max-width: 600px){
            width: 70%;
        }
    }
    .closeButton{
        cursor: pointer;
        top: 20px;
        left: 93%;
        position: absolute;
        width: 30px;
        border-bottom: 4px solid black;
        transform:rotate(45deg);
        @media (max-width: 600px){
            width: 20px;
            left: 90%;
        }
        &:before{
        content: '';
        position: absolute;
        width: 30px;
        left: 0;
        border-bottom: 4px solid black;
        // margin-top: 10px;
        transform:rotate(90deg);
        // top: 5px;
        @media (max-width: 600px){
            width: 20px;
        }
        }

    }
    .modalTitle{
        margin-top: 5%;
        font-size: 50px;
        @media (max-width: 600px){
            font-size: 29px;
        }
    }
    .modalOverwiew{
        font-size: 19px;
        padding: 4px;
        @media (max-width: 600px){
            font-size: 17px;
        }
    }
    .modalRating{
        font-weight: 900;
        font-size: 20px;
        margin: 30px 0;
        @media (max-width: 600px){
            font-size: 14px;
        }
    }
</style>
