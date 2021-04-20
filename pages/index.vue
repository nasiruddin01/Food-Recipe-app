<template>
  <div class="container">
    <div class="search">
      <input
        v-model="searchString"
        type="text"
        placeholder="Serch your recipe"
      />
      <button @click="searchMeals" class="btn">search</button>
    </div>
    <h2 v-if="searchedMeals">Sarched Meal</h2>
    <div v-for="meal in searchedMeals" :key="meal.idMeal" class="meal">
      <!-- <img :src="meal.strMealThumb" alt="" /> -->

      <div v-if="meal" class="header">
        <div class="about">
          <h1>Fish: {{ meal.strMeal }}</h1>
          <h4>{{ meal.strArea }}</h4>
          <h4 v-if="meal.strCategory">Food category: {{ meal.strCategory }}</h4>
          <h4 v-if="meal.strTags">Tag : {{ meal.strTags }}</h4>
        </div>
        <!-- <button @click="showDetails(meal)">show</button>
        {{ meal.showDetails }} value -->
        <!-- <template v-if="meal.showDetails"> -->
        <h3>Required Ingredient:</h3>
        <div class="ingredient">
          <template v-for="i in 20">
            <p v-if="meal['strIngredient' + i]" :key="'strIngredient' + i">
              {{ meal['strIngredient' + i] }}
              : {{ meal['strMeasure' + i] }}
            </p>
          </template>
        </div>
        <p class="instruction">{{ meal.strInstructions }}</p>
        <a :href="meal.strSource" target="_blank">Recipe source</a>
        <a :href="meal.strYoutube" target="_blank"
          ><svg
            aria-hidden="true"
            focusable="false"
            data-prefix="fab"
            data-icon="youtube"
            role="img"
            xmlns="http://www.w3.org/2000/svg"
            height="1rem"
            width="1.5rem"
            viewBox="0 0 576 512"
            class="svg-inline--fa fa-youtube fa-w-18 fa-5x"
          >
            <path
              fill="red"
              d="M549.655 124.083c-6.281-23.65-24.787-42.276-48.284-48.597C458.781 64 288 64 288 64S117.22 64 74.629 75.486c-23.497 6.322-42.003 24.947-48.284 48.597-11.412 42.867-11.412 132.305-11.412 132.305s0 89.438 11.412 132.305c6.281 23.65 24.787 41.5 48.284 47.821C117.22 448 288 448 288 448s170.78 0 213.371-11.486c23.497-6.321 42.003-24.171 48.284-47.821 11.412-42.867 11.412-132.305 11.412-132.305s0-89.438-11.412-132.305zm-317.51 213.508V175.185l142.739 81.205-142.739 81.201z"
              class=""
            ></path></svg
        ></a>
        <!-- </template> -->
      </div>
    </div>

    <h2 v-if="randomMeals">Random Meal</h2>
    <div v-if="randomMeals" class="random-meal">
      <!-- <img :src="randomMeals.strMealThumb" alt="" /> -->
      <div v-if="randomMeals" class="header">
        <div class="about">
          <h1>Fish: {{ randomMeals.strMeal }}</h1>
          <h4>{{ randomMeals.strArea }}</h4>
          <h4 v-if="randomMeals.strCategory">
            Food category: {{ randomMeals.strCategory }}
          </h4>
          <h4 v-if="randomMeals.strTags">Tag : {{ randomMeals.strTags }}</h4>
        </div>

        <h3>Required Ingredient:</h3>
        <div class="ingredient">
          <template v-for="i in 20">
            <p
              v-if="randomMeals['strIngredient' + i]"
              :key="'strIngredient' + i"
            >
              {{ randomMeals['strIngredient' + i] }}
              : {{ randomMeals['strMeasure' + i] }}
            </p>
          </template>
        </div>

        <p class="instruction">{{ randomMeals.strInstructions }}</p>
        <a :href="randomMeals.strSource" target="_blank">Recipe source</a>
        <a :href="randomMeals.strYoutube" target="_blank" class="youtube"
          ><svg
            aria-hidden="true"
            focusable="false"
            data-prefix="fab"
            data-icon="youtube"
            role="img"
            xmlns="http://www.w3.org/2000/svg"
            height="1rem"
            width="1.5rem"
            viewBox="0 0 576 512"
            class="svg-inline--fa fa-youtube fa-w-18 fa-5x"
          >
            <path
              fill="red"
              d="M549.655 124.083c-6.281-23.65-24.787-42.276-48.284-48.597C458.781 64 288 64 288 64S117.22 64 74.629 75.486c-23.497 6.322-42.003 24.947-48.284 48.597-11.412 42.867-11.412 132.305-11.412 132.305s0 89.438 11.412 132.305c6.281 23.65 24.787 41.5 48.284 47.821C117.22 448 288 448 288 448s170.78 0 213.371-11.486c23.497-6.321 42.003-24.171 48.284-47.821 11.412-42.867 11.412-132.305 11.412-132.305s0-89.438-11.412-132.305zm-317.51 213.508V175.185l142.739 81.205-142.739 81.201z"
              class=""
            ></path></svg
        ></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},

  data() {
    return {
      error: null,
      searchString: null,
      randomMeals: null,
      singleMeals: null,
      searchedMeals: null,
      // mutedMeals: [],
    }
  },
  computed: {
    classObject() {
      return {
        active: this.isActive && !this.error,
        'text-danger': this.error && this.error.type === 'fatal',
      }
    },
  },
  // watch: {
  //   searchedMeals: {
  //     deep: true,
  //     immediate: true,
  //     handler(value) {
  //       this.mutedMeals = JSON.parse(JSON.stringify(value))
  //       this.mutedMeals.map((meal) => {
  //         return meal
  //       })
  //     },
  //   },
  // },
  mounted() {
    this.fetchRandomMeals()
  },
  methods: {
    fetchRandomMeals() {
      const config = {
        method: 'get',
        url: `https://www.themealdb.com/api/json/v1/1/random.php`,
      }
      this.$axios(config)
        .then((response) => {
          this.randomMeals = response.data.meals[0]
        })
        .catch(function (error) {
          console.log(error)
        })
    },
    searchMeals() {
      const config = {
        method: 'get',
        url: `https://www.themealdb.com/api/json/v1/1/search.php?s=${this.searchString.trim()}`,
      }
      this.$axios(config)
        .then((response) => {
          this.searchedMeals = response.data.meals
          console.log(this.searchedMeals)
        })
        .catch(function (error) {
          console.log(error)
        })
    },
    // showDetails(meal) {
    //   this.searchedMeals.map((m) => {
    //     if (m.idMeal === meal.idMeal) {
    //       const dummy = JSON.parse(JSON.stringify(m))
    //       if (Object.hasOwnProperty(dummy, { showDetails: false })) {
    //         meal.showDetails = !meal.showDetails
    //       } else m.showDetails = false
    //     }
    //     return m
    //   })
    //   console.log('clicked', this.searchedMeals)
    // },
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/style.scss';
.container {
  max-width: 1080px;
  width: 90%;
  margin: 2rem auto 0 auto;
  .search {
    width: 100%;
    margin: 1rem auto;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    input {
      padding: 0.5rem 2rem;
      border-top-left-radius: 5px;
      border-bottom-left-radius: 5px;
    }
    .btn {
      padding: 0.5rem 2rem;
      border-top-right-radius: 5px;
      border-bottom-right-radius: 5px;
    }
  }
  .meal {
    display: grid;
    grid-template-columns: 1fr 30rem;
    grid-gap: 1rem;
    margin: 2rem 0;
    @media (max-width: 768px) {
      display: flex;
      flex-direction: column;
    }

    img {
      width: 35rem;
      border-radius: 5px;
      @media (max-width: 768px) {
        width: 100%;
      }
    }
    .header {
      h3 {
        margin-top: 1rem;
      }
      .ingredient {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-gap: 1rem;
        margin-top: 0.5rem;
        @media (max-width: 768px) {
          display: grid;
          grid-template-columns: 1fr 1fr;
          grid-gap: 1rem;
        }
        p {
          background: $color-border;
          font-size: 10px;
          display: flex;
          flex-direction: row;
          justify-content: center;
          align-items: center;
          padding: 0.5rem 0;
          border-radius: 5px;
        }
      }
      .instruction {
        margin: 1rem 0;
        line-height: 20px;
        @media (max-width: 768px) {
          text-align: center;
        }
      }
      a {
        text-decoration: none;
        color: #000;
      }
      .youtube {
        position: absolute;
        margin-left: 1rem;
      }
    }
  }
  h2 {
    text-align: center;
  }
  .random-meal {
    display: grid;
    grid-template-columns: 1fr 30rem;
    grid-gap: 2rem;
    margin-top: 2rem;
    padding-bottom: 2rem;
    @media (max-width: 768px) {
      display: flex;
      flex-direction: column;
    }
    img {
      width: 30rem;
      height: 100%;
      border-radius: 5px;

      @media (max-width: 768px) {
        width: 100%;
      }
    }
    .header {
      h3 {
        margin-top: 1rem;
      }
      .ingredient {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-gap: 1rem;
        margin-top: 0.5rem;
        @media (max-width: 768px) {
          display: grid;
          grid-template-columns: 1fr 1fr;
          grid-gap: 1rem;
        }
        p {
          background: $color-border;
          font-size: 10px;
          display: flex;
          flex-direction: row;
          justify-content: center;
          align-items: center;
          padding: 0.5rem 0;
          border-radius: 5px;
        }
      }
      .instruction {
        margin: 1rem 0;
        line-height: 20px;
      }
      .youtube {
        position: absolute;
        margin-left: 1rem;
      }
    }
  }
}
</style>
