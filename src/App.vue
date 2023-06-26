<template>
  <div class="row">
    <div class="card col border rounded shadow" v-for="(dogPic, index) in dogPics1">
      <img :src="dogPic" @click="toggleShowFront(1, index)" style="max-width: 25rem; max-height:20rem; margin-top: auto; margin-bottom: auto"
        v-show="selectedCardRow1 != index">
    
      <div v-for="(beatlesSong, index) in beatlesSongs1" v-if="selectedCardRow1 == index">
        <div class=" card col border rounded shadow" style="width: 23rem; height: 20rem" @click="toggleShowFront(1, index)" v-if="selectedCardRow1 == index">
          <div class="card-header">
            <p>Song Title - {{beatlesSong.title}}</p>
          </div>
          <div class="card-body">
            <p>Release Date - {{beatlesSong.date}}</p>
          </div>
          <div class="card-footer">
            <p>Song Writer - {{beatlesSong.writer}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>


  <br>
  <br>
  <div class="row">
    <div class="card col border rounded shadow" v-for="(dogPic, index) in dogPics2">
      <img :src="dogPic" @click="toggleShowFront(2, index)" style="max-width: 25rem; max-height:20rem; margin-top: auto; margin-bottom: auto"
        v-show="selectedCardRow2 != index">
    
      <div v-for="(beatlesSong, index) in beatlesSongs2" v-if="selectedCardRow2 == index">
        <div class=" card col border rounded shadow" style="width: 23rem; height: 20rem" @click="toggleShowFront(2, index)" v-if="selectedCardRow2 == index">
          <div class="card-header">
            <p>Song Title - {{beatlesSong.title}}</p>
          </div>
          <div class="card-body">
            <p>Release Date - {{beatlesSong.date}}</p>
          </div>
          <div class="card-footer">
            <p>Song Writer - {{beatlesSong.writer}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      selectedCardRow1: null,
      selectedCardRow2: null,
      dogPics1: {},
      dogPics2: {},
      beatlesSongs1: [
        { title: 'Let It Be', date: 'Mar 6 1970', writer: 'Lennon-McCartney' },
        { title: 'If I Needed Someone', date: 'Dec 3 1965', writer: 'Harrison' },
        { title: "Octopus's Garden", date: 'Sept 26 1969', writer: 'Starkey' },
        { title: 'Paperback Writer', date: 'June 10 1966', writer: 'Lennon-McCartney' },
        { title: 'Old Brown Shoe', date: 'May 30 1969', writer: 'Harrison' },
      ],
      beatlesSongs2: [
        { title: "Don't Pass Me By", date: 'Nov 22 1968', writer: 'Starkey' },
        { title: 'Fixing a Hole', date: 'June 1 1967', writer: 'Lennon-McCartney' },
        { title: "Don't Bother Me", date: 'Nov 22 1963', writer: 'Harrison' },
        { title: 'What Goes One', date: 'Dec 3 1965', writer: 'Lennon-McCartney-Starkey' },
        { title: 'For No One', date: 'Aug 5 1966', writer: 'Lennon-McCartney' }                
      ]

    }
  },
  async created(){
    const result1 = await fetch("https://dog.ceo/api/breeds/image/random/5");
    this.dogPics1 = await result1.json();
    this.dogPics1 = await JSON.parse(JSON.stringify(this.dogPics1)).message;

    const result2 = await fetch("https://dog.ceo/api/breeds/image/random/5");
    this.dogPics2 = await result2.json();
    this.dogPics2 = await JSON.parse(JSON.stringify(this.dogPics2)).message;

  },
  methods:{
    toggleShowFront(row, index){
      if(row == 1){
        if(this.selectedCardRow1 !=null){
          if(this.selectedCardRow1 == index){
            this.selectedCardRow1 = null;
          }
          else{
            this.selectedCardRow1 = index;
          }
        }
        else{
          this.selectedCardRow1 = index;
          this.selectedCardRow2 = null;
        }
      }
      else{
        if(this.selectedCardRow2 != null){
          if(this.selectedCardRow2 == index){
            this.selectedCardRow2 = null;
          }
          else{
            this.selectedCardRow2 = index;
          }
        }
        else{
          this.selectedCardRow2 = index;
          this.selectedCardRow1 = null;
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
