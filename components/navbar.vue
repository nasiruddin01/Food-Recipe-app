<template>
  <div class="container">
    <div class="navbar-container">
      <div class="logo"><span>F</span>oodi<span>W</span>orld</div>
      <div class="navbar">
        <p @click="fetchRandomMeals">Random meal</p>
      </div>
    </div>
  </div>
</template>
<style lang="scss" scoped>
@import '@/assets/style.scss';
.container {
  max-width: 100vw;
  width: 100%;
  box-shadow: 0px 0px 1px 0px $color-gray;
  position: fixed;
  background: #edecf0;
  .navbar-container {
    width: 90%;
    margin: 0 auto;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 1rem 0;

    @media (max-width: 1080px) {
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
      p {
        margin-top: 0.5rem;
      }
    }
  }
}
</style>
<script>
export default {}
</script>
