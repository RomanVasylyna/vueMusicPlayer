<template>
  <div id="app">

    <!-- Header Section  -->
  <header>
    <h1>My Music</h1>
  </header>
  
  <!-- Main Container For Elements -->
  <main>

  <!-- Player itself -->
  <section class="player">
    <h2 class="song-title">{{ current.title.toUpperCase() }} - 
    <span>{{ current.artist }}</span></h2>
  </section>

  <!-- Control Buttons -->
  <div class="controls">
   <button class="regular" @click="prevSong">Prev</button>
   <button class="play" @click="playMusic" v-if="!isPlaying">Play</button>
   <button class="play pause" @click="pause" v-else>Pause</button>
   <button class="regular" @click="nextSong">Next</button> 
  </div>

  <!-- Playlist Section -->
  <section class="playlist">
   <h2>The Playlist</h2>
   <p :key="song.src" v-for="song in songs" 
   @click="playMusic(song)"
   :class="(song.src == current.src) ? 'song-playing' : 'song'"
   >
   {{ song.title }} - {{ song.artist }}
   </p>
  </section>

  </main>

  </div>
</template>

<script>

export default {
  // Name of the app
  name: 'App',

  data() {
  return {
  
  // At first it's just an empty object
  current: {

  },
  
  // By default it's 0 (first song)
  index: 0,

  // Checking if the song is being played right now
  isPlaying : false,
  
  // Songs array
  songs: [

    {
     title: 'Deepsex',
     artist: 'Ellipse',
     src: require('./assets/ellipse - deepsex.mp3'), 
    },
    
    {
     title: 'Perfect Lady',
     artist: 'Made To Move',
     src: require('./assets/made to move - perfect lady.mp3'), 
    },

  ],
  
  // The way we handle audio
  player: new Audio(),




  }
  },
  
  // Lifecycle Hook (When element has been created)
  created() {  
  // current object = songs array of objects with index (which is currently 0)
  this.current = this.songs[this.index]; //So here the first song should appear
  // Setting Up Player's source
  this.player.src = this.current.src;
  // Songs starts playing right away
  // this.player.play();
  },

  methods: {
  
  // Start Playing Music
  playMusic(song) {  

  // If song's source is undefined
  if(typeof song.src != 'undefined') {
  // This current object = song
  this.current = song;
  // This player source = Current object source
  this.player.src = this.current.src;
  }
  
  this.player.play();
  this.isPlaying = true;
  },
  
  // Pause song
  pause() {
  this.player.pause();
  this.isPlaying = false;
  },
  
  // Play Next Song
  nextSong() {
  this.index++;  
  if(this.index > this.songs.length - 1) { //If index is longer then the last elem
  this.index = 0; //We are back to the first song
  }
  this.current = this.songs[this.index];
  this.playMusic(this.current);
  },

  // Play Prev Song
  prevSong() {
  this.index--;  
  if(this.index < 0) { //If index is longer then the last elem
  this.index = this.songs.length - 1; //We are back to the first song
  }
  this.current = this.songs[this.index];
  this.playMusic(this.current);
  }

  },
  
}
</script>

<style>
/* Basic Styling For all Elements */
*{
box-sizing: border-box;
margin: 0;
padding: 0;  
}

body{
font-family: sans-serif;
}

header{
display: flex; 
justify-content: center;
padding: 15px;
background: #212121;  
color: #fff;
}

main{
width: 100%;
margin: 25px auto;
}

.player{
text-align: center;
}

.controls{
display: flex;
flex-direction: row;
justify-content: center;
align-items: center;
margin-top: 20px;
}

.controls button{
font-weight: bold;
cursor: pointer;
}

.controls .regular{
background: rgb(231, 83, 83);
color: #fff;
padding: 8px 15px;
margin: 10px;
border-radius: 5px;
border: 0px;
}

.controls .play{
background: rgb(197, 11, 67);
color: #fff;
padding: 15px 20px;
margin: 10px;
border-radius: 5px;
border: 0px;
font-size: 1.2rem;
}

.playlist{
margin-top: 25px;  
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
}

.playlist h2{
padding: 10px;
}

.playlist .song{
padding: 10px; 
font-weight: bold; 
cursor: pointer;
font-size: 1.1rem;
width: 100%;
display: block;
text-align: center;
}

.playlist .song-playing{
 width: 100%; 
 padding: 10px; 
 font-weight: bold; 
 cursor: pointer;
 font-size: 1.1rem; 
 color: #fff;
 background-image: linear-gradient(to right, #CC2E5D, #FF5858); 
 text-align: center;
}

.playlist .song:hover{
color: #FF5858;  
}




</style>
