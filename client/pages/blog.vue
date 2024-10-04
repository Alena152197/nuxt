<template>
    <h1>Блог</h1>

    <main>
        <div class="posts">
            <article v-for="(post, index) in posts" :key="post.id">
                <h3>{{ post.title }}</h3>
                <img :src="base_url + post.img[0].url" :alt=post.img[0].alternativeText>
                <p>{{ post.desc }}</p>
                <NuxtLink :to="'/post/' + index">Подробнее</NuxtLink>
            </article>
        </div>

    </main>
</template>


<script setup>
const api = await $fetch('http://localhost:1337/api/posts?populate=*')
const posts = api.data

const base_url = "http://localhost:1337"
</script>


<style scoped>
.posts {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 25px;
}

@media screen and (max-width: 1024px) {
    .posts {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 25px;
    }
}

article {
    background-color: #f5f5f5;
    padding: 10px;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

article img {
    width: 100%;
}

article p {
    height: 100px;
}

article a {
    display: block;
}
</style>