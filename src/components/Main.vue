<template>
  <div class="wrapper">
    <!-- <Navbar /> -->
   <div class="container-fluid">
    <a name="example"></a>

  <Header />
        
    <div class="selection">
      <label class="font-weight-bold">Liga: </label>
      <dropdown  :options="liga" v-model="selectedLiga"></dropdown>
      <label class="font-weight-bold">Saison: </label>
      <dropdown :options="season" v-model="selectedSeason"></dropdown>
      <label class="font-weight-bold">Spieltag: </label>
      <dropdown :options="day" v-model="selectedDay"></dropdown>
    </div>
 
    <button type="button" class="btn btn-success btn-sm mt-2" v-on:click="showErgebnisse">Zeige Ergebnisse</button>
    <button type="button" class="btn btn-info btn-sm mt-2" v-on:click="showTabelle">Zeige Tabelle *</button>

    <p class="mt-3" v-if="wordList.length > 0 && clickedErg">Ergebnisse der {{wordList[0].LeagueName}}, {{wordList[0].Group.GroupName}}</p>
    
    <ListElements
    v-if="clickedErg"
      v-for="aword in wordList"
      v-bind:word="aword"
      v-bind:key="aword.id"
      />

      <Tabelle
         v-if="clickedTabelle"
         v-bind:thelist="tabelleList"
      />
   <Footer  v-if="clickedTabelle" v-bind:txt="tblmsg"/>
  </div> <!-- container fluid -->
  </div> <!--  wrapper -->
 
</template>

<script>
import ListElements from "./ListElements";
import Goal from "./Goal";
import Dropdown from "./Dropdown";
import Tabelle from "./Tabelle";
import Header from "./Header";
import Footer from "./Footer";

export default {
  name: "App",
  data() {
    return {
      wordList: [],
      tabelleList: [],
    
      selectedLiga: 'bl1',
      selectedSeason: '2013',
      selectedDay: '1',
  
      liga: {},
      season: [],
      day: [],

      clickedErg: false,
      clickedTabelle: false,

      tblmsg: '',

      // URL: "https://www.openligadb.de/api/getmatchdata/bl1/2016"
      URL: "https://www.openligadb.de/api/getmatchdata",
      TabelleURL: "https://www.openligadb.de/api/getbltable",
    };
  },
  computed:{
   
  },
  methods: {
    fillSelectMenus(){
      let currentYear = new Date().getFullYear();
      const currentMonth = new Date().getMonth();
      // month 8 is july 
      // starts 2003, current is new Date().getFullYear() aber vor neuer saison;
      if(currentMonth>7){
        currentYear++;
      }
      const startYear = 2003;
      const diff = currentYear - startYear;
      this.liga = Array(3).fill().map((e,i)=>({text: `${i+1}.Liga`, value: `bl${i+1}`}));
      this.season = Array(diff).fill().map((e,i)=>({text: `${i+startYear}/${i+startYear+1}`, value: i+startYear}));
      this.day = Array(34).fill().map((e,i)=>({text: `${i+1}.Spieltag`, value: i+1}));
      // this.liga = {'1.Liga':'bl1','2.Liga':'bl2'};
    },
    showErgebnisse() {
      this.clickedErg = true;
      this.clickedTabelle = false;
      const theUrl = `${this.URL}/${this.selectedLiga}/${this.selectedSeason}/${this.selectedDay}`;
      console.log(theUrl);
      fetch(theUrl)
        .then(res => res.json())
        .then(data => (this.wordList = data))
        .catch(err => console.log(err));
    },
    showTabelle() {
      this.clickedTabelle = true;
      this.clickedErg = false;
      const theTabelleUrl = `${this.TabelleURL}/${this.selectedLiga}/${this.selectedSeason}`;
      console.log(theTabelleUrl);
      fetch(theTabelleUrl)
        .then(res => res.json())
        .then(data => {
            this.tabelleList = data;
            this.tblmsg = '*  beendete Spielzeiten: Tabelle letzter Spieltag';
        })
        .catch(err => console.log(err));
    },
 
  },
  created() {
    this.fillSelectMenus();
  },
  components: {
    ListElements,
    Goal,
    Dropdown,
    Tabelle,
    Header,
    Footer
  }
};
</script>

<style>
 .wrapper{
    max-width: 800px;
 }

 #headingOne, .card-header{
  
   width: 100%;
 }

@media screen and (max-width: 420px) {
 #headingOne, .card-header{
   margin-left: 0 !important;
   /* background: aqua; */
   padding-left: 0 !important;
   /* min-width: 330px !important;
   max-width: 345px !important; */
   width: 100%;
 }
 label{
   display: none;
 }
}
</style>
