<template>
  <div class="container">
    <div class="navbar-container">
      <a href="https://foodiworld.netlify.app/" class="logo"
        ><span>F</span>oodi<span>W</span>orld</a
      >
      <div class="navbar">
        <a href="saved-meals">Saved Recipe</a>
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
  z-index: 100;
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
      text-decoration: none;
      span {
        color: #ffa36c;
      }
    }
    .navbar {
      a {
        margin-top: 0.75rem;
        text-decoration: none;
        font-weight: 600;
        color: #000;
      }
    }
  }
}
</style>
<script>
export default {}
</script>
