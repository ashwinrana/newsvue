<template>
    <div>
        <router-link :to="`/detail/${id}`" @click="readnews"><img :src="thumbnailUrl" class="card-img-top" :alt="title">
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <p class="card-text">{{ description }}</p>
        </div>
        <div class="card-footer">
            <small class="text-muted">Pusblised at: {{ moment(created_at, 'YYYYMMDD').fromNow() }}</small>
        </div>
        </router-link>
    </div>
</template>

<script>
export default {
    name: 'NewsCard',
    props: [
        'id', 'title', 'description', 'thumbnailUrl', 'created_at'
    ],
}
</script>