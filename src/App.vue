<template>
  <div id="app">

  <!-- Top Header -->
  <header>
    <h1>My Music</h1>
  </header>

  <!-- Main Section -->
  <main>
    <!-- Song Title -->
   <h3> {{current.title}} - <span>{{current.artist}}</span></h3>

   <!-- Player Controls -->
   <section class="controls">
   <button class="prev" @click="prevTrack">Prev</button>
   <button class="play" @click="playMusic" v-if="!isPlayed">Play</button>
   <button class="play" @click="pause" v-else>Pause</button>
   <button class="next" @click="nextTrack">Next</button>
   </section>

   <!-- Playlist -->
   <!--  :class=" (current.src == player.src) ? 'song-playing' : 'song'" -->
   <section class="playlist">
   <h2>The Playlist</h2>
   <p :key="song.src"
   v-for="song in songs"
   :class=" (current.src == song.src) ? 'song-playing' : 'song'"
   >{{song.title}} - {{song.artist}}</p>
   </section>

  </main>

  </div>
</template>

<script>

export default {
  name: 'App',

  data() {
  return {

  // Here we store currently playing song
  current: {

  },

  // Songs Array
  songs: [
  {
   title: 'Deep Sex',
   artist: 'Ellipse',
   src: require('./assets/ellipse - deepsex.mp3')
  },

  {
   title: 'Perfect Lady',
   artist: 'Made to Move',
   src: require('./assets/made to move - perfect lady.mp3')
  }
  ],

  player: new Audio(),

  isPlayed : false,

  index: 0,



  }
  },

  methods: {

  // Start Playing current song
  playMusic() {
  this.player.play();
  this.isPlayed = true;
  },

  pause() {
  this.player.pause();
  this.isPlayed = false;
  },

  // Play Next Track
  nextTrack() {
  // Increase index
  this.index++;
  // Make sure index is not bigger than the last array elem
  if(this.index > this.songs.length - 1) {
  this.index = 0;
  }
  // Putting current track into the current object
  this.current = this.songs[this.index];
  // Put current src into player
  this.player.src = this.current.src;
  // Play the track
  this.player.play();
  this.isPlayed = true;
  },

  // Functionality is the same as for nextTrack but backwards
  prevTrack() {
  this.index--;
  if(this.index < 0) {
  this.index = this.songs.length - 1;
  }
  this.current = this.songs[this.index];
  this.player.src = this.current.src;
  this.player.play();
  this.isPlayed = true;
  }

  },

  // Lifecycle Hook (Created)
  created() {
  //Placing first song in the current object
  this.current = this.songs[this.index];

  // Assigning song src to the player object
  this.player.src = this.current.src;
  },


}
</script>

<style>
/* Basic Styling */
*{
box-sizing: border-box;
margin: 0;
padding: 0;
}

/* Font Style for the document */
body{
font-family: sans-serif;
}

header{
background: black;
color: #fff;
display: flex;
justify-content: center;
align-items: center;
}

header h1{
margin: 10px auto;
}

main{
margin: 25px ;
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
}

main h3{
font-size: 1.4rem;
text-transform: uppercase;
color: rgb(59, 59, 59);
font-weight: 700;
}

/* Player Buttons Styling */
.controls button{
margin: 22px 10px;
font-weight: bold;
}

.controls .prev, .next{
color: #fff;
background: rgb(235, 79, 79);
border: 0px;
border-radius: 5px;
padding: 8px 15px;
}

.controls .play{
color: #fff;
background: rgb(141, 1, 59);
padding: 15px 25px;
border: 0px;
border-radius: 5px;
font-size: 1.2rem;
}

.playlist{
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
}

.playlist h2{
margin: 12px auto;
}

.playlist p{
margin: 5px;
font-size: 1.1rem;
}

.playlist .song:hover{
color: #FF5858;
}

.playlist .song-playing{
 background-image: linear-gradient(to right, #CC2E5D, #FF5858);
color: #fff;
}





</style>
