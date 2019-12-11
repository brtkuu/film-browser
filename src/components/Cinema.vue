<template>
    <div class="wrapper">
    </div>
</template>
<script>
export default {
  name: 'Cinema',
};
</script>
<style lang="scss" scoped>
.wrapper{
    position: fixed;
    top: 0;
    left: 0;
    height: 100vh;
    width: 100%;
    z-index: -1;
    background-image: url('../assets/cinemahall.png');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    @media (max-width: 600px) {
    background-image: url('../assets/smallbcg.jpg');
    }
}
</style>
