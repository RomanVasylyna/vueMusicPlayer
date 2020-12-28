<template>
  <div id="app">

    <!-- Header Section -->
  <header>
    <h1>My Music</h1>
  </header>

  <!-- Player itself -->
  <section class="player">
    <h2 class="song-title">{{ current.title.toUpperCase() }} - 
    <span>{{ current.artist }}</span></h2>
  </section>

  <!-- Control Buttons -->
  <div class="controls">
   <button class="regular">Prev</button>
   <button class="play" @click="playMusic">Play</button>
   <button class="regular" @click="nextSong">Next</button> 
  </div>

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
  playMusic() {
  this.player.play();
  },

  nextSong() {
  this.index++;  
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

.player{
text-align: center;
margin-top: 20px;
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


</style>
