<template>
  <div>
    <main>
      <Nuxt />
    </main>    
  </div>
</template>

<script>
export default {
}
</script>

<style lang="scss">
  main{
    width: 80%;
    margin-left: 10%;
  }
  @media (max-width: 700px) {
    main{
      width: 90%;
      margin-left: 5%;
    }
  }
</style>
