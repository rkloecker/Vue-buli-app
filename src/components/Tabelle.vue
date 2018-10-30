<template>
<div>
<!-- Beschriftung -->
   <div v-if="thelist.length>0" class="row beschr mt-2 no-gutters sm-font">
 <div class="col-8 col-sm-5 vereine">Verein</div> 
    <div class="col-1 text-center">Spiele</div> 
    <div class="col-2 text-center dsbl-1">S/U/N</div>
    <div class="col-1 text-center">Punkte</div>
    <div class="col-2 text-center">Tore</div>
    <div class="col-1 text-center dsbl">Diff</div>
     
  </div>

  <div 
   v-for="(tbl, index) in thelist"
    
      v-bind:key="tbl.TeamInfoId"
  id="tbl" class="row no-gutters  font-normal"> 
    <div class="col-8 col-sm-5 vereine">{{index+1}}. {{tbl.TeamName}} </div> 
    <div class="col-1 text-center"> {{tbl.Matches}}</div> 
    <div class="col-2 text-center dsbl-1">{{tbl.Won}}/{{tbl.Draw}}/{{tbl.Lost}}</div>
    <div class="col-1 text-center">{{tbl.Points}}</div>
    <div class="col-2 text-center">{{tbl.Goals}}:{{tbl.OpponentGoals}}</div>
    <div class="col-1 text-center dsbl">{{tbl.GoalDiff}}</div>
  </div> 

</div>
</template>

<script>
export default {
  props: ["thelist"]
};
</script>

<style scoped>
.sm-font {
  font-size: 0.9em;
  font-weight: bold;
  /* background-color: #f2f2f2; */
  border-bottom: 1px solid #ddd;
}

@media screen and (max-width: 576px) {
.sm-font {
  font-size: 0.6em;
  font-weight: bold;
  /* background-color: #f2f2f2; */
  border-bottom: 1px solid #ddd;
}
.font-normal {
  font-size: 1em;
}
.no-gutters {
  margin-right: 0;
  margin-left: 0;
}

.col,
[class*="col-"] {
  padding-right: 0;
  padding-left: 0;
  margin-right: 0;
  margin-left: 0;
}
 .dsbl,.dsbl-1 {
   display: none;
 }
}

@media screen and (min-width: 421px) {
.font-normal {
  font-size: 1.0em;
}
}

@media screen and (min-width: 471px) and (max-width: 575px){
.dsbl-1 {
   display: inherit;
 }
  .dsbl {
   display: none;
 }
 .vereine{
   max-width:50% !important;
 }
}
</style>

