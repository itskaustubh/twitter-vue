<template>
  <div id="app">
    <div class='nav'>
      <div id='nav-logo'>SocialFeed</div>
      <div id='nav-id'>kaustubh</div>
    </div>
    <router-view/>
  </div>
</template>

<script>


export default {
  name: 'App',
}
</script> 

<style lang='scss'>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  /* min-height: 100vh; */
  background-color: #F3F5FA;
}

.nav{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 15px 5%;
  background-color: lightcyan;  

  #nav-logo{
    font-size: 24px;
    color:lightseagreen;
    font-weight: bold;
    font-style: italic;
  }

  #nav-id{
    font-weight: bold;
    font-size: 20px;
  }
}
</style>
