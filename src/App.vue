<template>
  <div id="app">
  
  <!-- Top Header -->
  <header>
    <h1>My Music</h1>
  </header>
  
  <!-- Main Section -->
  <main>
    <!-- Song Title -->
   <h3>Song Title - <span> Song Artist</span></h3> 

   <section class="controls">
   <button>Prev</button>  
   <button>Play</button>
   <button>Pause</button>
   <button>Next</button>
   </section>

  </main>

  </div>
</template>

<script>

export default {
  name: 'App',
  
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



</style>
