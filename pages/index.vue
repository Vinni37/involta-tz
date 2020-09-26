<template>
  <div>
    <Navbar 
      v-bind:type-sourse ='type_sourse'
      v-bind:show-images ='show_images'
      
      v-on:change-sourse='changeSourse'
      v-on:change-find-text='changeFindText' 
      v-on:reload-rss='reloadRSS'
      v-on:change-type-view= 'changeTypeView'      
    />
    <div class="newsImages" v-if="show_images">
      <CardImage
        v-for ='news in view_news' :key='news.title[0]'
        v-bind:news ='news'
      />
    </div>
    <div class="news" v-else>
      <Card
        v-for ='news in view_news' :key='news.title[0]'
        v-bind:news ='news'
      />
    </div>
    <Paginated
      v-bind:count-page = count_page
      v-bind:page-number = page_number
      v-on:change-page='changePage'
    />
    <div>
      <a href="https://github.com/Vinni37/involta-tz" target="_blank">Ссылка на github</a>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Card from '@/components/Card.vue';
import CardImage from '@/components/CardImage.vue';
import Paginated from '@/components/Paginated.vue';

export default {
  data: function(){
    return{
      news_mos: null,
      news_len: null,
      post_on_page: 4,
      type_sourse: 'all',
      show_images: false,
      page_number: 1,
      search_text: ''   
    }    
  },
  mounted(){
    this.loadRSS();
  },
  computed: {
    view_news: function(){
      if (this.filtered_news === null) return null;
      return this.filtered_news.slice(this.page_number*this.post_on_page - this.post_on_page, this.page_number*this.post_on_page)
    },
    filtered_news: function(){
      // Добавить фильтр по тексту
      let temp_news = this.all_sourse_news;
      let search_text = this.search_text;
      if (temp_news === null) return null;
      if (this.search_text != ""){
        temp_news = temp_news.filter(function(temp_new){
          if (temp_new.title[0].indexOf(search_text)>-1) return true
          else return false;
        })
      }
      return temp_news;
    },
    all_sourse_news: function(){
      if (this.news_mos === null || this.news_len === null) return null
      else {
        switch (this.type_sourse) {
          case 'lenta':            
            return this.news_len;
            break;
          case 'mos':
            return this.news_mos;
            break;            
          default:
            return this.news_mos.concat(this.news_len);
            break;
        }        
      }
    },
    count_page: function(){
      if (this.news_mos === null || this.news_len === null) return 0
      else {
        let count_page = Math.ceil(this.filtered_news.length / this.post_on_page);
        if (this.page_number > count_page) this.page_number = count_page;
        return count_page;
      }
    }
  },
  methods:{
    loadRSS: async function(){
      // https://www.mos.ru/rss => https://involta.mypn.ru/rss
      // https://lenta.ru/rss/news => https://involta.mypn.ru/news
      const xml2js = require('xml2js');
      let news_mos_xml = await this.$axios.$get('rss');
      let news_len_xml = await this.$axios.$get('news');
      xml2js.parseString(news_mos_xml, function (err, result) {
        news_mos_xml = result.rss.channel[0].item;
      });
      xml2js.parseString(news_len_xml, function (err, result) {
        news_len_xml = result.rss.channel[0].item;
      });
      this.news_mos = news_mos_xml;
      this.news_len = news_len_xml;
    },
    changePage:function(data){
      this.page_number = data.pageNumber
    },
    changeSourse:function(data){      
      this.type_sourse = data.typeSourse
    },
    changeFindText:function(data){
      this.search_text = data.findText;
    },
    reloadRSS:function(){
      this.loadRSS();
    },
    changeTypeView:function(data){
      if (data.show_images) {
        this.post_on_page = 3
      } else {
        this.post_on_page = 4
      }
      this.show_images = data.show_images
    }
  }
}
</script>

<style lang="scss" scoped>
  .newsImages, .news {
    margin-top: 1rem;
  }
  .news{
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
  body{
    background: #e5e5e547;
  }
  @media (max-width: 700px) {
    .news{
      display: block;
    }
  }
</style>
