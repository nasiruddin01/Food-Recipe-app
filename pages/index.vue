<template>
  <div class="container">
    <h1 class="main-header">Popular Food</h1>
    <p>
      We provide a variety of food and beverage recipes <br />
      with high test from famous chefs
    </p>
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
      <div v-if="meal" class="header">
        <div class="about">
          <h1>{{ meal.strMeal }}</h1>
          <h4>
            <span>Origin: {{ meal.strArea }} •</span>
            <span v-if="meal.strCategory"
              >Food category: {{ meal.strCategory }}</span
            >
          </h4>
          <a :href="meal.strYoutube" target="_blank" class="youtube"
            >Recipe is live here</a
          >
          <img :src="meal.strMealThumb" alt="" />
          <h4 v-if="meal.strTags">Tag : {{ meal.strTags }}</h4>
        </div>
        <h3>Required Ingredient:</h3>
        <div class="ingredient">
          <table>
            <tr>
              <th>Ingredient</th>
              <th>Quantity</th>
            </tr>
            <template v-for="i in 20">
              <tr
                class="table-row"
                v-if="meal['strIngredient' + i]"
                :key="'strIngredient' + i"
              >
                <td>{{ meal['strIngredient' + i] }}</td>
                <td>{{ meal['strMeasure' + i] }}</td>
              </tr>
            </template>
          </table>
        </div>

        <p class="instruction">{{ meal.strInstructions }}</p>
        <a :href="meal.strSource" target="_blank" class="source"
          >Recipe source</a
        >
      </div>
    </div>

    <h2 v-if="randomMeals">Random Meal</h2>
    <div v-if="randomMeals" class="meal">
      <div v-if="randomMeals" class="header">
        <div class="about">
          <h1>Food type: {{ randomMeals.strMeal }}</h1>

          <h4>
            <span>Origin: {{ randomMeals.strArea }}.</span>
            <span v-if="randomMeals.strCategory"
              >Food category: {{ randomMeals.strCategory }}</span
            >
          </h4>

          <a :href="randomMeals.strYoutube" target="_blank" class="youtube"
            >Recipe is live here</a
          >
          <img :src="randomMeals.strMealThumb" alt="" />
          <h4 v-if="randomMeals.strTags">Tag : {{ randomMeals.strTags }}</h4>
        </div>

        <h3>Required Ingredient:</h3>
        <div class="ingredient">
          <table>
            <tr>
              <th>Ingredient</th>
              <th>Quantity</th>
            </tr>
            <template v-for="i in 20">
              <tr
                v-if="randomMeals['strIngredient' + i]"
                :key="'strIngredient' + i"
                class="table-row"
              >
                <td>{{ randomMeals['strIngredient' + i] }}</td>
                <td>{{ randomMeals['strMeasure' + i] }}</td>
              </tr>
            </template>
          </table>
        </div>

        <p class="instruction">{{ randomMeals.strInstructions }}</p>
        <a :href="randomMeals.strSource" target="_blank" class="source"
          >Recipe source</a
        >
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
  margin: 2rem auto 0 auto;
  .main-header {
    text-align: center;
    font-size: 3rem;
    font-weight: 300;
  }
  p {
    text-align: center;
    margin-top: 1rem;
    font-size: 16px;
    line-height: 20px;
  }
  @media (min-width: 769px) {
    margin: 0 auto;
  }
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
      border: 1px solid $color-tertiary;
    }
    input:focus {
      border: none;
      outline: 1px solid $color-tertiary;
    }
    .btn {
      padding: 0.5rem 2rem;
      border-top-right-radius: 5px;
      border-bottom-right-radius: 5px;
      border: 1px solid $color-tertiary;
    }
    .btn:focus {
      outline: 1px solid $color-tertiary;
    }
    .btn:hover {
      border: none;
      outline: 1px solid $color-tertiary;
    }
  }

  h2 {
    text-align: center;
    margin-bottom: 1rem;
  }
  .meal {
    background: #edecf0;
    border-radius: 5px;
    border: 1px solid $color-tertiary;
    padding: 1rem;
    width: 90%;
    max-width: 700px;
    margin: auto;
    margin-bottom: 2rem;

    .header {
      width: 95%;
      margin: 0 auto;
      padding-top: 0.5rem;
      @media (max-width: 768px) {
        width: 95%;
      }
      h3 {
        margin-top: 1rem;
      }
      .about {
        h4 {
          margin-bottom: 2rem;
        }
        .youtube {
          text-decoration: none;
          color: #000;
          background: #ffa36c;
          padding: 0.5rem 1rem;
          border-radius: 5px;
        }
        img {
          width: 100%;
          border-radius: 5px;
          margin: 1rem 0 1rem 0;
          @media (max-width: 768px) {
            width: 100%;
          }
        }
      }
      .ingredient {
        margin-top: 1rem;
        table {
          margin: auto;
          border: 1px solid #b3b3b3;
          width: 100%;
          max-width: 1000px;
          border-collapse: collapse;
          .table-row {
            border-collapse: collapse;
          }
          tr:nth-child(odd) {
            text-align: start;
          }

          th,
          td {
            padding: 0.5rem 1rem;
            color: black;
            border: 1px solid black;
            // text-align: center;
          }
        }
      }
      .instruction {
        margin: 1rem 0;
        line-height: 20px;
      }
      .source {
        text-decoration: none;
        color: #000;
        background: #ffa36c;
        padding: 0.5rem 1rem;
      }
    }
  }
}
</style>
