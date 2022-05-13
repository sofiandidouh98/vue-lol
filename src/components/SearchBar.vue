<script setup>
import { Search } from '@element-plus/icons'
</script>

<template>
  <div class="grid-container">
    <div></div>
    <div><img src="https://opgg-static.akamaized.net/logo/20220419150536.c51b7aadeb324fcf8039f954c31fedc2.png?image=q_auto,f_webp,w_auto&amp;v=1651555450322" style="height: 200px;" alt="OP.GG logo (Ivern)" title="Ivern"></div>
    <div></div>
  </div>
    
    <el-input
      v-model="input"
      placeholder="Buscar jugador"
      class="input-with-select"
      type="text"
    >
    <template #append>
        <el-button :icon="Search" @click="searchSummoner"/>
    </template>
    </el-input>

        <img :src="summoner.avatar" style="height: 250px;">
        <h1>{{summoner.name}}</h1><br>
        <el-tag type="success">{{summoner.summonerLevel}}</el-tag>

 <!--<pre>{{ JSON.stringify(this.summoner, null, 2) }}</pre>
 <hr>-->

</template>

<script>

    export default {
        data() {
            return {
                input:'',
                summoner:{},
                league:{},
            }
        },
    methods:{
        searchSummoner:async function(){
            const response = await fetch(`https://euw1.api.riotgames.com/lol/summoner/v4/summoners/by-name/${this.input}`,{
                headers:{
                    'X-Riot-Token' : 'RGAPI-851a6adc-fec4-4a19-9d9d-12c01cc613a6'
                }
            })
            const data = await response.json()
            const avatar = `http://ddragon.leagueoflegends.com/cdn/12.8.1/img/profileicon/${data.profileIconId}.png`;
            const rango = `https://euw1.api.riotgames.com/lol/league/v4/entries/by-summoner/${data.id}`;
            this.summoner={...data, avatar, rango};
        }, 

        searchLeague:async function(){
            const response = await fetch(`https://euw1.api.riotgames.com/lol/league/v4/entries/by-summoner/${this.input}`,{
                headers:{
                    'X-Riot-Token' : 'RGAPI-851a6adc-fec4-4a19-9d9d-12c01cc613a6'
                }
            })
            const data = await response.json()          

            this.league={data};
        }
    }

    }
    
</script>

<style>
img{
    margin-top: 20px;
    align-content: center;
}
#el-tag{
margin-top: -100px;
}
pre{
    text-align: center;
}

.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  gap: 10px;
  padding: 10px;
  margin-top: 30px;

}

.grid-container > div {
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
}
</style>