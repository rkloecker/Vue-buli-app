<template>
 <div class=" mb-2 ">

 <div id="accordion">
  <div class="card">
    <div class="card-header" id="headingOne">
      <h5 class="mb-0">
        <button class="btn btn-link" data-toggle="collapse" :data-target="`#${word.MatchID}`" aria-expanded="true" aria-controls="collapseOne">
          
             <div class="teams">
               <img :src="word.Team1.TeamIconUrl" alt="" @error="imageLoadError" >
               {{word.Team1.TeamName}} : 
               <img :src="word.Team2.TeamIconUrl" alt="" @error="imageLoadError" >
               {{word.Team2.TeamName}}  {{result}} 
     <!-- <button class="btn btn-info btn-sm" @click="showDetails">Details</button> -->
     </div>
        </button>
      </h5>
    </div>

    <div :id="word.MatchID" v-bind:class="{ collapse: isLoaded }" aria-labelledby="headingOne" data-parent="#accordion">
      <div class="card-body">

 <MatchInfo v-on:close="closeIt()" v-bind:info="word"/>
       
<div class="">
  <ul class="list-group list-group-flush">
 <Goal
      v-for="item in word.Goals"
      v-bind:goal="item"
      v-bind:key="item.id"
      />
  </ul>
  </div>

      </div>
    </div>
  </div>
</div>

 </div>

</template>

<script>
import Goal from "./Goal";
import MatchInfo from "./MatchInfo";

export default {
  props: ["word"],
  data() {
    return {
      clicked: false,
      isLoaded: true
    };
  },
  methods: {
    showDetails() {
      this.clicked = true;
      this.$emit("details", this.clicked);
    },
    closeIt() {
      this.clicked = false;
    },
    
    imageLoadError() {
      console.log("Image failed to load");
      this.word.Team1.TeamIconUrl = '../assets/logo.png';
    }
  },

  beforeUpdate() {
    // $('.collapse').collapse();
    console.log("before update");
    //  console.log($('.collapse'));
    $(".show").removeClass("show");
  },
  computed: {
    // a computed getter
    result: function() {
      let key = 0;
      if (this.word.MatchResults[1] && this.word.MatchResults[1].ResultTypeID == 2) {
        key = 1;
      }
      return `${this.word.MatchResults[key].PointsTeam1}:${
        this.word.MatchResults[key].PointsTeam2
      }`;
    }
  },
  components: {
    Goal,
    MatchInfo
  }
};
</script>

<style scoped>
 .teams{
   font-size: 3vw;
 }



@media screen and (max-width: 360px) {
 .teams{
   /* font-size: 3vw; */
   font-size: 7px;
   font-size: 0.65em;
 }

}

img {
  max-height: 20px;
  margin-right: 5px;
  margin-left: 5px;
  margin-bottom: 2px;
}
.grid-striped .row:nth-of-type(odd) {
  background-color: rgba(0, 0, 0, 0.05);
}

 @media screen and (min-width: 1100px) {
  .teams{
   /* font-size: 2vw; */
   font-size: 1rem;
 }
 }
</style>
