<template>
  <div class="inner" v-if="info.Location">
    <span v-if="info.Location && info.Location.LocationCity">{{info.Location.LocationCity}}, </span>
    <span v-else></span>
    <span v-if="info.Location && info.Location.LocationStadium">{{info.Location.LocationStadium}}, </span>
    <span v-else></span>
    <span class="font-weight-bold" v-if="info.NumberOfViewers">{{info.NumberOfViewers}} Zuschauer</span>
    <span v-else></span>

  </div>
</template>

<script>
export default {
  props: ['info'],
}
</script>

<style scoped>
   .inner {
  width: 100%;
  margin: 0 auto;
  margin-bottom: 10px;
  font-size: 0.8em;
  padding-bottom: 0.5em;
  padding-left: 1.5em;
   margin-bottom: 5px;
    border-bottom: 1px solid #eee;
}

 @media screen and (max-width: 420px) {
 .inner {
  width: 100%;
  padding-bottom: 0.5em;
  padding-left: 1.5em;
  margin: 0 auto;
  margin-bottom: 5px;
  font-size: 3vw;
  border-bottom: 1px solid #eee;
}
}
</style>


