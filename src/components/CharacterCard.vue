<template>
    <div class="character__wrapper">

        <div class="character__loader" v-if="loading">
            <img src="/static/img/loader.svg" alt="Loading">
        </div>

        <div class="character__card" v-for="(character, index) in characters" :key="index" v-on:click="activeCard(index)" v-bind:class="{active: index === activeItem}">
            
            <h2 class="character__card__title">{{character.name}}</h2>

            <div class="character__card__photo">
                <img :src="character.thumbnail.path+'.'+character.thumbnail.extension">
                
            </div>

            <div class="character__card__footer">
                <div class="character__card__info" v-bind:class="{active: index === activeItem}">
                    <p class="character__card__info__title"></p>
                    <p class="character__card__info__value"><span class="character__card__info__unit">%</span></p>
                </div>
                <div class="character__card__info" v-bind:class="{active: index === activeItem}">
                    <p class="character__card__info__title"></p>
                    <p class="character__card__info__value"><span class="character__card__info__unit">hPa</span></p>
                </div>
                <div class="character__card__updated">
                    <!-- Updated at: {{updatedAt}} -->
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import axios from 'axios';

var PUBLIC_KEY = "94645aeeb126295ca095d5ddbb091a54";
var hash = "3fe15284862d243a6b6931c1e1405f34";

export default {
    data(){
        return{
            characters: '',
            loading: true,
            tempVal: '',
            updatedAt: '',
            activeItem: 1,
        }
    },
    created(){
        this.getCharacters()
        // window.clearInterval(this.interval)
        // this.interval = window.setInterval(() => this.makeRequest(), 600000);
    },
    methods: {
        activeCard(index){
             this.activeItem = index;
        },
        getActualDate(){
            let d = new Date();
            let currentDate =  d.toLocaleTimeString('pt-BR', {hour12: true});
            this.updatedAt = currentDate;
        },
        tempColor(tempValue){
            if(tempValue <= 5){
                return 'blue';
            } else if(tempValue > 26){
                return 'red';
            } else {
                return 'orange';
            }
        },
        getCharacters(){
             axios
            .get('https://gateway.marvel.com:443/v1/public/characters?orderBy=modified&limit=6&ts=1&apikey=94645aeeb126295ca095d5ddbb091a54&hash=3fe15284862d243a6b6931c1e1405f34')
            .then(res => {
                console.log(res.data.data.results);
                this.characters = res.data.data.results;
                // this.weathers = res.data.list;
                // this.loading = false;
                // this.getActualDate();
            })
            .catch(error => {
                console.log(error)
                this.errored = true
            })
            .finally(() => this.loading = false)
        }
    },
}
</script>

<style lang="postcss">
.character__loader {
  position: fixed;
  top: 50%;
  left: 50%;
  margin-left: -25px;
  margin-top: -25px;
}
.character__card {
  height: 220px;
  border-radius: 5px;
  background-color: #fff;
  margin-bottom: 28px;
  box-shadow: 2px 2px 5px 0px rgba(51, 51, 51, 0.1);
  transition: all 0.2s ease-in-out;
  &.active {
    height: 272px;
  }
  &__title {
    height: 42px;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.8rem;
    color: #737c84;
    border-bottom: 1px solid #ebebeb;
  }
  &__photo {
    height: 138px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3rem;
    position: relative;
    img {
      max-width: 100%;
      max-height: 100%;
      height: auto;
    }
    sup {
      font-size: 5rem;
      margin-top: -25px;
    }
    &.blue {
      color: #69a3ff;
    }
    &.orange {
      color: #ff9632;
    }
    &.red {
      color: #ed1946;
    }
  }
}
.character__card__footer {
  min-height: 42px;
  background-color: rgba(241, 241, 241, 0.5);
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
}
.character__card__info {
  width: 100%;
  display: none;
  flex-direction: column;
  align-items: center;
  &.active {
    display: flex;
  }
  &__title {
    color: #b4b4b4;
    text-transform: uppercase;
    font-size: 1.2rem;
    padding-top: 14px;
    padding-bottom: 6px;
  }
  &__value {
    color: #737c84;
    font-size: 1.6rem;
  }
  &__unit {
    font-size: 1.1rem;
  }
}
.character__card__updated {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 40px;
  color: #b4b4b4;
  font-size: 1rem;
}

@media (orientation: landscape) {
  .character__card {
    width: 270px;
    margin: 0 auto 28px;
  }
}
@media (min-width: 768px) {
  .character__card {
    width: 270px;
    margin: 0 auto 28px;
  }
}
@media (min-width: 890px) {
  .character__wrapper {
    display: flex;
    width: 100%;
    min-height: 350px;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
  }
  .character__card {
    width: 255px;
    margin: 0 auto 28px;
    transition: all 0.2s ease-in-out;
    &.active {
      transform: scale(1.1);
      transition: all 0.2s ease-in-out;
    }
  }
}
</style>


