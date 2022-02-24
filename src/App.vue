<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Rank from './components/Rank.vue'
import axios from 'axios'
import usersData from "./../saveData.json";
import { reactive, ref } from 'vue'
const rank = usersData.rank;
const baseURL = "http://localhost:3001/";
const region = 'euw'
const api_key = 'RGAPI-49f53b1c-b8cb-4727-aebf-483eb785f233'
const query = ref('LPA Wayzis')

async function saveData(data, endpoint) {
  try {
    const res = await axios.post(`${baseURL}${endpoint}`, data);
    console.log(res);
  } catch (error) {
    console.error(error);
  }

}
async function getSummonerId(pseudo) {
  const apiString = `https://euw1.api.riotgames.com/lol/summoner/v4/summoners/by-name/${pseudo}?api_key=${api_key}`
  console.log('call');
  return await axios.get(apiString)
    .then(res => res.data)
    .then(res => {
      saveData(res, 'summoner')
      console.log(res)
      return res
    })
}
async function getRank(summonerId) {
  const apiString = `https://euw1.api.riotgames.com/lol/league/v4/entries/by-summoner/${summonerId}?api_key=${api_key}`
  console.log('call');
  return await axios.get(apiString)
    .then(res => res.data)
    .then(res => {
      saveData(res[0], 'rank')
      console.log(res)
      return res
    })
}
</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <Rank :data="rank" />
  <form @submit.prevent="changeNome(query)">
    <input v-model="query" />
    <button @click="submit">Search</button>
  </form>
  <button @click="saveData()">sdqdsqd</button>
</template>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #dde2e7;
  background: rgba(8, 8, 26, 0.541);
  margin-top: 60px;
}
</style>
