<template>
  <div class="container">
    <h1 class="main-header">Popular Food</h1>
    <p class="text">
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
      <Meal :meal="meal" />
    </div>
    <div class="btn-container">
      <button @click="fetchRandomMeals" class="random-btn">Random Meal</button>
    </div>

    <h2 v-if="randomMeals">Random Meal</h2>
    <div v-if="randomMeals" class="meal">
      <Meal :meal="randomMeals" />
    </div>
  </div>
</template>

<script>
import Meal from '~/components/meal.vue'
export default {
  components: { Meal },
  data() {
    return {
      error: null,
      searchString: null,
      randomMeals: null,
      singleMeals: null,
      searchedMeals: null,
      // saveMeals: null,
      // addNewMeal: null,
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
  margin: 0 auto 0 auto;
  padding-top: 4rem;
  .main-header {
    text-align: center;
    font-size: 3rem;
    font-weight: 300;
  }
  .text {
    text-align: center;
    margin-top: 1rem;
    font-size: 16px;
    line-height: 20px;
    @media (max-width: 768px) {
      width: 95%;
      font-size: 14px;
      margin: 0 auto;
    }
  }
  @media (min-width: 769px) {
    width: 95%;
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
      padding: 0.5rem 1rem;
      border-top-left-radius: 3px;
      border-bottom-left-radius: 3px;
      border: 1px solid $color-tertiary;
    }
    input:focus {
      border: none;
      outline: 1px solid $color-tertiary;
      border-radius: 3px;
    }
    .btn {
      padding: 0.5rem 2rem;
      border-top-right-radius: 3px;
      border-bottom-right-radius: 3px;
      border: 1px solid $color-tertiary;
    }
    .btn:focus {
      outline: 1px solid $color-tertiary;
      border-radius: 3px;
    }
  }
  .btn-container {
    width: 100%;
    margin: 0 auto;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    .random-btn {
      text-decoration: none !important;
      color: #000 !important;
      background: #ffa36c !important;
      padding: 0.5rem 1rem !important;
      border-radius: 3px !important;
      border: none;
      outline: none;
    }
  }

  h2 {
    text-align: center;
    margin: 1rem 0;
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
    padding-bottom: 2.5rem;
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
        div {
          display: flex;
          flex-direction: row;
          justify-content: space-between;
          h1 {
            margin-bottom: 1rem;
          }
          button {
            border: none;
            outline: none;
            font-size: 16px;
            font-weight: 600;
            svg {
              transform: translateY(2px);
            }
          }
        }
        h4 {
          margin-bottom: 1rem;
        }
        .youtube {
          text-decoration: none;
          color: #000;
          font-weight: 600;
          svg {
            transform: translateY(2px);
          }
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
        margin: 1.5rem 0;
        line-height: 20px;
      }
      .source {
        text-decoration: none;
        color: #000;
        background: #ffa36c;
        padding: 0.5rem 1rem;
        border-radius: 3px;
      }
    }
  }
}
</style>
