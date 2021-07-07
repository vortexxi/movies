<template>
  <header>
    <router-link to="/">
      <h3>MOVIES INFO</h3>
    </router-link>
  </header>
  <main>
    <router-view/>
  </main>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Bangers&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Anton&family=Roboto+Mono:ital,wght@0,300;0,400;0,500;1,700&display=swap');
  *{
    padding:0px;
    margin: 0px;
    box-sizing: border-box;
  }
  body{
    /*background-color: #B7AC44;*/
    background-color: #000;
  }
  header{
    background-color: #000;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 48px;
    font-family: 'Anton', sans-serif;
    /*font-family: 'Bangers', cursive;*/
    font-size: 24px;
    z-index: 10;
  }
  a{
    color:#FF4500;
    text-decoration: none;
  }
</style>

