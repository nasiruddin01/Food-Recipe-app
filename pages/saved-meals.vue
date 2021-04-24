<template>
  <div class="saved-meal">
    <h1>Recipe you have saved</h1>
    <template v-if="savedMeals">
      <div v-for="meal in savedMeals" :key="meal.idMeal" class="meal">
        <Meal :meal="meal" :isSaved="true" @meal-deleted="onDelete" />
      </div>
    </template>
  </div>
</template>

<script>
import Meal from '~/components/meal.vue'

export default {
  components: { Meal },
  data() {
    return {
      savedMeals: null,
    }
  },
  created() {
    this.savedMeals = JSON.parse(localStorage.getItem('meals'))
  },
  methods: {
    onDelete() {
      this.savedMeals = JSON.parse(localStorage.getItem('meals'))
    },
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/style.scss';
.saved-meal {
  padding-top: 6rem;
  max-width: 700px;
  width: 90%;
  margin: 0 auto;
  h1 {
    text-align: center;
    padding-bottom: 1rem;
  }
}
.meal {
  background: #edecf0;
  border-radius: 5px;
  border: 1px solid $color-tertiary;
  padding: 1rem;
  width: 100%;
  max-width: 700px;
  margin: auto;
  margin: 2rem 0;
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
</style>
