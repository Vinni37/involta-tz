<template>
  <section>
      <div class="card">
        <h1>{{news.title[0]}}</h1>
        <p>{{news.description[0]}}</p>
        <a v-bind:href=news.link[0] target="_blank">Подробнее</a>
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
    section {
        box-shadow: 0px 2px 5px 0px rgba(34, 60, 80, 0.2);
        background: white;
        margin: 0.5rem;
    }
    .card {
      padding: 2rem;
    }
    .card h1 {
      color: #0029FF;  
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
</style>