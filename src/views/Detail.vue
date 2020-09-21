<template>
  <div>
    <!-- Start news details here.-->
    <div class="text-center">
    <div class="news-title">
        {{ news.title }}
    </div>
    <div class="news-publised-time">
      Published at: {{moment(news.created_at, 'YYYYMMDD').fromNow() }}
    </div>
    <div class="news-image">
      <img :src="news.image_url" :alt="`${news.title} image`">
    </div>
    <div class="news-detail text-justify mx-auto">
      {{ news.description }}
    </div>
    </div>
    <!-- End news details here.-->
    <!-- Start related news here.-->
    <div class="related-news">
      <div class="card-deck">
        <div class="card" v-for="list in relatedNews" :key="list.id">
          <NewsCard :id="list.id" :title="list.title" :description="list.description" :thumbnailUrl="list.thumbnailUrl" :created_at="list.created_at" />
        </div>
      </div>
    </div>
    <!-- End  related news here.-->

  </div>
</template>
<script>
import axios from 'axios'
import NewsCard from '@/components/NewsCard.vue'

export default {
    name: 'Details',
    components: {
      NewsCard
    },
    props: [ 'id'],
    data() {
        return {
            news:[],
            relatedNews:[]
        }
    },
    async created() {
    try {
      
      const res = await axios.get(`http://localhost:3000/news/` + this.$route.params.id)
      this.news = res.data;

      /**
      * Get Current Data's tags 
      */
      const tags = this.news.tags;

      /**
       * Retrive the related news based on the first tag of the current news.
       */
      const related = await axios.get(`http://localhost:3000/news/?tags.title=` + tags[0].title + `&_sort=id&_order=desc&id_ne=` + this.$route.params.id +`&_limit=5`)
      
      this.relatedNews = related.data;
    } catch(e) {
      if(e.response.status == 404) {
        this.$router.push({ name: '404' })
      }
    }
  },
}
</script>
<style scoped>
  .news-title {
    font-size: 25px;
  }

  .news-image {
    margin-top: 18px;
  }

  .news-detail {
    margin-top: 18px;
    margin-bottom: 18px;
  }
</style>