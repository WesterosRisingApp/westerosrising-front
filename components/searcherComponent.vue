<!-- eslint-disable vue/first-attribute-linebreak -->
<template>

  <v-card class=" got card--desktop" elevation="5">
    <div :class="character.house" class="mt-0">
      <div v-if="character.image">
        <v-img class="image mt-0" max-height="620px" :lazy-src="imageDefault" :src="character.image" />
      </div>
      <div v-else>
        <v-img class="image mt-0" max-height="300px" :src="imageDefault" />
      </div>
      <v-card-title class="mb-8">
        <h4 class="h4 text-md-h3"> {{character.name}}</h4>
      </v-card-title>
      <v-card-subtitle class="mb-4 end">
        <div v-if="doesHouseExist()">
          <v-img :src="checkMyHouse()" width="50px" height="50px" class="absolute" />
        </div>
        <div v-else>
          <v-img :src="shieldDefault" width="50px" height="50px" class="absolute" />
        </div>
        <h2>{{character.house}}</h2>
      </v-card-subtitle>
      <v-card-text>
        <div v-if="checkMyTitles()">
          <h5>TITLES</h5>
          <div v-for="(titles, idx) in character.titles" :key="idx">
            <p> {{titles}}</p>
          </div>
        </div>
        <div v-if="character.gender == 'male'">
          <h5>GENDER</h5>
          <p>Male</p>
        </div>
        <div v-else-if="character.gender == 'drake'">
          <h5>GENDER</h5>
          <p>Drake</p>
        </div>
        <div v-else>
          <h5>GENDER</h5>
          <p>Female</p>
        </div>
        <div v-if="character.alive">
          <h5>STATE</h5>
          <p> Alive</p>
        </div>
        <div v-else>
          <h5>STATE</h5>
          <p> Dead</p>
        </div>
        <div v-if="character.culture">
          <h5>CULTURE</h5>
          <p>{{character.culture}}</p>
        </div>
      </v-card-text>
    </div>
  </v-card>

</template>

<script>

import defaultImage from '@/assets/imgs/imgNotFound.png'
import defaultShield from '@/assets/imgs/shieldNotFound.png'
export default {
  name: 'SearcherComponent',
  props: {
    // eslint-disable-next-line vue/require-default-prop
    character: {
      type: Object
    }
  },
  data() {
    return {
      imageDefault: defaultImage,
      shieldDefault: defaultShield,
      housesValidated: ['House Stark', 'House Arryn', 'House Baratheon', 'House Greyjoy', 'House Lannister', 'House Martell', 'House Targaryen', 'House Targaryen[1]', 'House Tully', 'House Tyrell'],
      houseImg: {
        default: defaultShield,
        "House Stark": require(`~/assets/shields/House Stark.png`),
        "House Arryn": require(`~/assets/shields/House Arryn.png`),
        "House Baratheon": require(`~/assets/shields/House Baratheon.png`),
        "House Greyjoy": require(`~/assets/shields/House Greyjoy.png`),
        "House Lannister": require(`~/assets/shields/House Lannister.png`),
        "House Martell": require(`~/assets/shields/House Martell.png`),
        "House Targaryen": require(`~/assets/shields/House Targaryen.png`),
        "House Targaryen[1]": require(`~/assets/shields/House Targaryen.png`),
        "House Tully": require(`~/assets/shields/House Tully.png`),
        "House Tyrell": require(`~/assets/shields/House Tyrell.png`),
      }
    }
  },
  methods: {
    doesHouseExist() {
      return this.housesValidated.includes(this.character.house)
    },
    checkMyHouse() {

      if (this.houseImg[`${this.character.house}`] || this.character.house !== 'Westeros Rising') {
        return this.houseImg[`${this.character.house}`]
      }

      return this.houseImg.default
    },
    checkMyTitles() {
      return this.character.titles
    }
  }
}
</script>

<style scoped>
.image {
  border-radius: 4px 4px 0px 0px;
  margin-top: 0;
  object-position: top !important;
}

p {
  margin-left: 15px;
}


@font-face {
  font-family: 'TheanoOldStyle-Regular';
  src: url('../assets/fonts/TheanoOldStyle-Regular.ttf') format('truetype');
}

.got {
  text-decoration: none;
  font-family: 'TheanoOldStyle-Regular' !important;
}

.Stark {
  border: 2px solid #808080 !important;

}

.Arryn {
  border: 2px solid #cecece !important;
}

.Tully {
  border: 2px solid #af2824 !important;
}

.Greyjoy {
  border: 2px solid rgb(235, 202, 20) !important;
}

.Lannister {
  border: 2px solid #af9710 !important;
}

.Baratheon {
  border: 2px solid #000000 !important;
}

.Tyrell {
  border: 2px solid #8d840a !important;
}

.Martell {
  border: 2px solid #8f2424 !important;
}

.Targaryen {
  border: 2px solid #770f0f !important;
}

.absolute {
  position: absolute;
  margin-top: -10px;
}

h3,
h2 {
  margin-left: 25%;
}

@media (min-width: 800px) {

  .card--desktop {
    margin: auto;
  }

  h5 {
    font-size: x-large;
    margin-bottom: 1em;
  }

  p {
    margin-bottom: 2rem;
    font-size: x-large;
  }
}
</style>
