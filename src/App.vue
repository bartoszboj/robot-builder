<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li class="nav-item">
            <img class="logo" src="./assets/build-a-bot-logo.png" alt="">
            <span>build-a-bot</span>
          </li>
        </ul>
      </nav>
    </header>
    <main>
      <robot-builder></robot-builder>
    </main>
  </div>
</template>

<script>
// import HomePage from '@/components/home/HomePage.vue';
import RobotBuilder from '@/components/builder/RobotBuilder.vue';

export default {
  name: 'App',
  components: {
    // HomePage,
    RobotBuilder
  }
}
</script>

<style lang="scss">

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    font-family: 'Roboto', sans-serif;
    background: linear-gradient(to bottom, #555, #999);
    background-attachment: fixed;
    user-select: none;
  }
</style>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

  main {
    margin: 0 auto;
    padding: 30px;
    background-color: white;
    max-width: 1280px;
    min-height: 300px;
  }

  header {
    background-color: #999;
    max-width: 1280px;
    margin: 0 auto;
    padding: 10px;

    span{
      margin-left: 10px;
      
    }
    .nav-item {
      display: inline-block;
      padding: 5px 10px 5px 0;
      font-size: 22px;
      border-right: 1px solid #bbb;
    }
    .logo {
      vertical-align: middle;
      height: 30px;
    }
    .ul {
      padding: 3px;
      display: flex;
      padding-inline-start: 0;
    }
  }
</style>
