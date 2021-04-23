<template>
  <div class="saved-meal">
    <h1>Recipe you have saved</h1>
    <template v-if="savedMeals">
      <div v-for="meal in savedMeals" :key="meal" class="meal">
        <div v-if="meal" class="header">
          <div class="about">
            <div>
              <h1>{{ meal.strMeal }}</h1>
            </div>

            <h4>
              <span>Origin: {{ meal.strArea }} &nbsp;•&nbsp; </span>
              <span v-if="meal.strCategory"
                >Category: {{ meal.strCategory }}</span
              >
            </h4>
            <a :href="meal.strYoutube" target="_blank" class="youtube"
              ><svg
                aria-hidden="true"
                focusable="false"
                data-prefix="fab"
                data-icon="youtube"
                role="img"
                xmlns="http://www.w3.org/2000/svg"
                height="16px"
                viewBox="0 0 576 512"
                class="svg-inline--fa fa-youtube fa-w-18 fa-5x"
              >
                <path
                  fill="red"
                  d="M549.655 124.083c-6.281-23.65-24.787-42.276-48.284-48.597C458.781 64 288 64 288 64S117.22 64 74.629 75.486c-23.497 6.322-42.003 24.947-48.284 48.597-11.412 42.867-11.412 132.305-11.412 132.305s0 89.438 11.412 132.305c6.281 23.65 24.787 41.5 48.284 47.821C117.22 448 288 448 288 448s170.78 0 213.371-11.486c23.497-6.321 42.003-24.171 48.284-47.821 11.412-42.867 11.412-132.305 11.412-132.305s0-89.438-11.412-132.305zm-317.51 213.508V175.185l142.739 81.205-142.739 81.201z"
                  class=""
                ></path>
              </svg>
              &nbsp;Recipe is live here</a
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
            >Recipe Source</a
          >
        </div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  data() {
    // data saving in localhost method
    return {
      savedMeals: null,
    }
  },
  created() {
    this.savedMeals = JSON.parse(localStorage.getItem('meals'))
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
