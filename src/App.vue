<template>
<div id="app">
  <header>
    <h1>My Music</h1>
  </header>
  <main>
    <section class="player">
      <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
      <div class="controls">
        <button class="prev" @click="prev">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next" @click="next">Next</button> 
      </div>
    </section>
    <section class="playlist">
      <h3>Playlist</h3>
      <button v-for="song in songs" :key="song.src" @click="play(song)"
      :class="(song.src == current.src) ? 'song playing' : 'song'">
      {{ song.title }} - {{ song.artist }}
      </button>
    </section>
  </main>
</div>

</template>
     
<script>


export default {
  name: 'App',
  components: {
    
  },
  data(){
    return{
      current: {
        
      },
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'City High',
          artist: 'Inspectah Deck x Ras Stone',
          src: require('./assets/city.mp3')
        },
        {
          title: 'Interstella Era',
          artist: 'Ras Stone',
          src: require('./assets/era.mp3')
        },
        {
          title: 'Land of The Free',
          artist: 'Ras Stone x Joey B@dass',
          src: require('./assets/land.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play(song){
      if (typeof song.src != "undefined"){
        this.current =song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause(){
      this.player.pause();
      this.isPlaying = false;
    },
    next(){
      this.index++;
      if(this.index > this.songs.length -1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
        this.play(this.current);
    },
    prev(){
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length -1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    this.player.play();
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: sans-serif;
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}
</style>
