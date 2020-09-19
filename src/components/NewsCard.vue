<template>
    <div>
        <img :src="thumbnailUrl" class="card-img-top" :alt="title">
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <p class="card-text">{{ description }}</p>
        </div>
        <div class="card-footer">
            <small class="text-muted">Created at 3 mins ago</small>
        </div>
    </div>
</template>

<script>
export default {
    name: 'NewsCard',
    props: [
        'id', 'title', 'description', 'thumbnailUrl'
    ],
}
</script>