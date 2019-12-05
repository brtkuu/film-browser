<template>
<div class="modalWrapper">
    <h1 class="modalTitle"> {{ modalInfo.title }} </h1>
    <p class="modalOverwiew"> {{ modalInfo.overview }}</p>
    <p class="modalRating"> Rating: {{ modalInfo.vote_average }}
    <div class="closeButton" v-on:click="$emit('closeButton')"></div>
</div>
</template>
<script>
export default {
  name: 'Modal',
  props: ['modalInfo'],
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
    }
    .closeButton{
        cursor: pointer;
        top: 20px;
        left: 93%;
        position: absolute;
        width: 30px;
        border-bottom: 4px solid black;
        transform:rotate(45deg);
        &:before{
        content: '';
        position: absolute;
        width: 30px;
        left: 0;
        border-bottom: 4px solid black;
        // margin-top: 10px;
        transform:rotate(90deg);
        // top: 5px;
        }
    }
    .modalTitle{
        margin-top: 5%;
        font-size: 50px;
    }
    .modalOverwiew{
        font-size: 19px;
    }
    .modalRating{
        font-weight: 900;
        font-size: 20px;
        margin: 30px 0;
    }
</style>
