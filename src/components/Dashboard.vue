<template>
  <div class="dashboard">
    <div class="score score-left">{{ wins.zero }}</div>
    <span class="separator"></span>
    <div class="score score-right">{{ wins.cross }}</div>
  </div>
</template>

<script>
import player from '../assets/playersType';

export default {

  props: {
    wins: player,
  },
  name: 'Dashboard',
};
</script>

<style>
  .dashboard {
    display: flex;
    flex-direction: row;
    justify-content: center;
    font-size: 1.4em;
    color: #ffffff;
  }

  .separator {
    position: relative;
    content: '';
    width: 20px;
    background-color: #2c3e50;
  }

  .score {
    padding: 15px 0;
    width: 100%;
    vertical-align: bottom;
  }

  .score-left {
    border-radius: 15px 0 0 0;
    background-color: #f1c40f;
  }

  .score-right {
    border-radius: 0 15px 0 0;
    background-color: #217ad3;
  }
</style>
