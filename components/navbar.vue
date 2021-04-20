<template>
  <div class="container">
    <div class="navbar-container">
      <div class="logo"><span>F</span>oodi<span>W</span>orld</div>
      <div class="navbar">
        <p>Home</p>
        <p>Meal</p>
        <p @click="randomMeals">Random meal</p>
        <div @click="searchMeals" class="search-bar">
          <input type="text" placeholder="Search your recipe" />
          <div>
            <svg
              aria-hidden="true"
              focusable="false"
              data-prefix="fas"
              data-icon="search"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              height="12px"
              width="12px"
              viewBox="0 0 512 512"
              class="svg-inline--fa fa-search fa-w-16 fa-5x"
            >
              <path
                fill="currentColor"
                d="M505 442.7L405.3 343c-4.5-4.5-10.6-7-17-7H372c27.6-35.3 44-79.7 44-128C416 93.1 322.9 0 208 0S0 93.1 0 208s93.1 208 208 208c48.3 0 92.7-16.4 128-44v16.3c0 6.4 2.5 12.5 7 17l99.7 99.7c9.4 9.4 24.6 9.4 33.9 0l28.3-28.3c9.4-9.4 9.4-24.6.1-34zM208 336c-70.7 0-128-57.2-128-128 0-70.7 57.2-128 128-128 70.7 0 128 57.2 128 128 0 70.7-57.2 128-128 128z"
                class=""
              ></path>
            </svg>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="scss" scoped>
@import '@/assets/style.scss';
.container {
  max-width: 100vw;
  width: 100%;
  box-shadow: 0px 1px 0px 0px $color-border;

  .navbar-container {
    width: 90%;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 50rem 1fr;
    grid-gap: 1rem;
    padding: 1rem 0;
    @media (max-width: 768px) {
      width: 90%;
      grid-template-columns: auto 1fr;
      grid-gap: 1rem;
    }
    .logo {
      font-size: 25px;
      font-weight: 600;
      span {
        color: #ffa36c;
      }
    }
    .navbar {
      display: grid;
      grid-template-columns: auto auto 1fr 1fr;
      grid-gap: 1rem;
      .search-bar {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        @media (max-width: 768px) {
          display: none;
        }
        input {
          padding: 0.25rem 1rem;
          border: none;
          outline: none;
        }
        div {
          transform: translateX(-11.5rem);
          padding-left: 0.5rem;
          svg {
            color: $color-tertiary;
          }
          // width: 2rem;
        }
      }
    }
  }
}
</style>
<script>
export default {
  setup() {},
}
</script>
