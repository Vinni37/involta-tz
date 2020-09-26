<template>
  <section> 
    <div class="card">
      <img v-bind:src=this.news.enclosure[0].$.url>
      <div>
        <h1>{{news.title[0]}}</h1>
        <p>{{news.description[0]}}</p>
      </div>
    </div>
      <div class="footer">
        <a v-bind:href=origin>{{host_name}}</a>
        {{news.pubDate[0]}}
      </div>
  </section>
</template>

<script>
export default {
    props: ['news'],
    computed: {
      host_name: function(){
          return new URL(this.news.link[0]).hostname;
      },
      origin: function(){
          return new URL(this.news.link[0]).origin;
      }
    }
}
</script>

<style lang="scss" scoped>
  section{
    box-shadow: 0px 2px 5px 0px rgba(34, 60, 80, 0.2);
    background: white;
    margin-bottom: 1rem;
  }
  .card{
    display: flex;
    padding: 2rem;
  }
  .card img {
    width: 20%; 
  }
  .card h1 {
    color: #0029FF;  
  }
  .card div {
    margin: 1rem;
  }

  .footer {
    display: flex;
    background: #FCFCFC;
    justify-content:space-between;
    padding: 1rem 2rem 1rem 2rem;
    color: #DCDCDC;
  }
  .footer a {
    color: #DCDCDC;
  }
  @media (max-width: 700px) {
    .card{
      display: block;
      padding: 1rem;
    }
    .card img {
      width: 100%;
    }
    .footer {
      padding: 1rem 1rem 1rem 1rem;
    }
    .card div {
      margin: 0;
    }
  }
</style>