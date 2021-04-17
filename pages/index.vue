<template>
  <div class="container">
    <div class="search">
      <input v-model="searchString" type="text" />
      <button @click="searchMeals">search</button>
    </div>
    <div v-for="meal in searchedMeals" :key="meal.idMeal" class="meal">
      <img :src="meal.strMealThumb" alt="" />
      <div v-if="searchedMeals" class="searched-meal">
        <div v-if="meal" class="single-meal">
          <h1>{{ meal.strMeal }}</h1>

          <h4>{{ meal.strArea }}</h4>
          <h4 v-if="meal.strCategory">
            Food category: '{{ meal.strCategory }}'
          </h4>

          <h4 v-if="meal.strTags">Tag : {{ meal.strTags }}</h4>
          <p v-for="i in 20" :key="'strIngredient' + i">
            {{ searchMeals['strIngredient' + i] }}
            <span v-if="searchMeals['strIngredient' + i]">:</span>
            {{ searchMeals['strMeasure' + i] }}
          </p>

          <p>{{ meal.strInstructions }}</p>
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
        </div>
      </div>
    </div>
    <div class="random-meal">
      <img :src="randomMeals.strMealThumb" alt="" />
      <div v-if="randomMeals" class="header">
        <h1>Fish: {{ randomMeals.strMeal }}</h1>
        <h4>{{ randomMeals.strArea }}</h4>
        <h4 v-if="randomMeals.strCategory">
          Food category: {{ randomMeals.strCategory }}
        </h4>

        <h4 v-if="randomMeals.strTags">Tag : {{ randomMeals.strTags }}</h4>
        <p v-for="i in 20" :key="'strIngredient' + i">
          {{ randomMeals['strIngredient' + i] }}
          <span v-if="randomMeals['strIngredient' + i]">:</span>
          {{ randomMeals['strMeasure' + i] }}
        </p>

        <p>{{ randomMeals.strInstructions }}</p>
        <a :href="randomMeals.strSource" target="_blank">Recipe source</a>
        <a :href="randomMeals.strYoutube" target="_blank"
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
      <!-- <div v-if="randomMeals.strMealThumb" class="img">
        <img :src="randomMeals.strMealThumb" alt="" />
      </div> -->
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
  }
  .meal {
    display: grid;
    grid-template-columns: 1fr 30rem;
    grid-gap: 1rem;
    margin-bottom: 2rem;
    img {
      width: 35rem;
    }
  }
  .random-meal {
    display: grid;
    grid-template-columns: 1fr 30rem;
    grid-gap: 2rem;
    img {
      width: 35rem;
    }
  }
}
</style>
