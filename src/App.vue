<template>
<div id="app">
  <header>
    <h1>My Music</h1>
  </header>
  <main>
    <section class="player">
      <h2 class="song-title">{{ current.title }} <span>{{ current.artist }}</span></h2>
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
      songs: [
        {
          title: 'City High [Ras Stone Remake]',
          artist: 'Inspectah Deck x Ras Stone',
          src: require('./assets/city.mp3')
        },
        {
          title: 'Interstella Era',
          artist: 'Ras Stone',
          src: require('./assets/era.mp3')
        },
        {
          title: 'LAnd of The Free',
          artist: 'Ras Stone x Joey B@dass',
          src: require('./assets/land.mp3')
        }
      ],
      player: new Audio()
    }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
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
