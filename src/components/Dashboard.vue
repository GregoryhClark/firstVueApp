<template>
  <div class="body">
    <h1>I Choose You!</h1>
      <div>
      <select v-model="choice1" >
        <option>-select-</option>
        <option v-for='x in pokemon2' :key='x.name'>{{x.name}}</option>
        </select>
    <button @click="getPokemonDetails()">
     get your pokemon!!</button>
      <select v-model="choice2">
        <option>-select-</option>
        <option v-for='x in pokemon2' :key='x.name'>{{x.name}}</option>
        </select>
        </div>
<div>
    {{choice1}}
    <button @click='getStats()'>getStats</button>
    {{choice2}}
</div>
<div>
  {{stat1}}
<button @click='fight()'>Fight</button>
  {{stat2}}
</div>
<br/>
{{winner}}
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Dashboard",
  props: {
    msg: String
  },
  data() {
    return {
      firstName: "luke",
      pokemon: [],
      pokemon2: "",
      filteredShips: [],
      choice1: '',
      choice2: '',
      stat1: '',
      stat2: '',
      winner: '',
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon/")
      .then(res => this.pokemon.push(res.data.results));
  },
  methods: {
    getPokemonDetails() {
      this.pokemon2 = this.pokemon[0];
      console.log(this.pokemon2);
    },
    getStats(){
      axios.get(`${this.pokemon2.filter(x=>x.name===this.choice1)[0].url}`).then(res=>this.stat1 = res.data.stats[0].base_stat)
      axios.get(`${this.pokemon2.filter(x=>x.name===this.choice2)[0].url}`).then(res=>this.stat2 = res.data.stats[0].base_stat)
      console.log(this.stat1, this.stat2);
            
    },
    fight(){
      if (this.stat1 > this.stat2){
        this.winner = `${this.choice1} is the winner!!!`
      }
      else if (this.stat1 < this.stat2){
        this.winner = `${this.choice2} is the winner!!!!`
      }
      else if (this.stat1 = this.stat2){
        this.winner = 'TIE!!!!!!!!!!!'
      }
      console.log('something');
      
    }
  
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.body{
  height: 900px;
  background: rgb(163, 10, 10);

}
.stuff{
  background: black;
}
h1{
  color: white;
  font-size: 100px;
}
div{
  color: white;
  font-size: 50px;
}
</style>
