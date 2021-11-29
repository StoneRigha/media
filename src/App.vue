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
        },
        {
          title: 'Lunar Shrill',
          artist: 'Ras Stone',
          src: require('./assets/Ras Stone.mp3')
        },
        {
          title: 'Celestial Hypnosis',
          artist: 'Ras Stone',
          src: require('./assets/Ras Stone_2.mp3')
        },
        {
          title: '26 Forever',
          artist: 'Ras Stone',
          src: require('./assets/26.mp3')
        },
        {
          title: 'I Want Peace',
          artist: 'Ras Stone',
          src: require('./assets/peace.mp3')
        },
        {
          title: 'Idle End',
          artist: 'Ras Stone',
          src: require('./assets/idle.mp3')
        },
        {
          title: 'Difference',
          artist: 'Ras Stone',
          src: require('./assets/diff.mp3')
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
      this.player.addEventListener('ended', function(){
         this.index++;
      if(this.index > this.songs.length -1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
        this.play(this.current);
      }.bind(this));
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
main{
  width: 100%;
  max-width: 768px;
  margin: 0px auto;
  padding: 25px;
}
.song-title{
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  font-family: cursive;
  text-transform: uppercase;
  text-align: center;
}
.song-title span{
  font-weight: 400;

}
.controls{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button{
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover{
  opacity: 0.8;
}
.play, .pause{
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #cc285d;
}
.next, .prev{
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #ff5858;
}
.playlist{
  padding: 0px 30px;
}
.playlist h3{
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover{
  color: #ff5858;
}
.playlist .song.playing{
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5b, #ff5858);
}
</style>
