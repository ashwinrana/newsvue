<template>
  <div class="card-deck">
    <div class="card" v-for="list in lists" :key="list.id">
      <NewsCard :title="list.title" :description="list.description" :thumbnailUrl="list.thumbnailUrl" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src'
import NewsCard from '@/components/NewsCard.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    NewsCard
  },
  data() {
    return {
      lists: []
    }
  },
  async created() {
    try {

      // TODO: Remove limit after resolving the CSS issue in the home page
      const res = await axios.get(`http://localhost:3000/news?_limit=5`)

      this.lists = res.data;
    } catch(e) {
      console.error(e)
    }
  },
}
</script>
