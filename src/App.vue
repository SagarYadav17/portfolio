<script>
import BlogPostCard from './components/BlogPostCard.vue';

export default {
    name: 'App',
    data() {
        return {
            blogPosts: null, blog_domain: import.meta.env.VITE_BLOG_DOMAIN
        }
    },
    async mounted() {
        let query = `
        {
            user(username: "${import.meta.env.VITE_HASHNODE_USERNAME}") {
                publication {
                    posts(page: 0) {
                        slug
                        title
                        dateAdded
                        brief
                    }
                }
            }
        }`;
        try {
            let res = await fetch('https://api.hashnode.com/', {
                method: 'POST',
                headers: {
                    'content-type': 'application/json',
                },
                body: JSON.stringify({ query }),
            });
            res = await res.json();
            const response = res.data;
            this.blogPosts = response?.user?.publication?.posts;
        } catch (error) {
            console.log(error);
        }
    },
};

</script>



<template>
    <header aria-label="Page Header">
        <div class="mx-auto max-w-screen-xl px-4 py-8 sm:px-6 sm:py-12 lg:px-8">
            <div class="sm:flex sm:items-center sm:justify-between">
                <div class="text-center sm:text-left">
                    <h1 class="text-2xl font-bold text-gray-900 sm:text-3xl">
                        Work in progress
                    </h1>

                    <p class="mt-1.5 text-sm text-gray-500">
                        Meanwhile, you can check out some of my blog posts.
                    </p>
                </div>
            </div>
        </div>
    </header>

    <div class="p-10 grid grid-cols-1 sm:grid-cols-1 md:grid-cols-3 lg:grid-cols-3 xl:grid-cols-3 gap-5">
        <div class="rounded overflow-hidden shadow-lg" v-for="post in  blogPosts ">
            <div class="px-6 py-4">
                <a :href="blog_domain + post.slug" class="font-bold text-xl mb-2">{{ post.title }}</a>
                <p class="text-gray-700 text-base">
                    {{ post.brief }}
                </p>
            </div>
            <div class="px-6 pt-4 pb-2">
                <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">
                    {{ post.dateAdded }}</span>
            </div>
        </div>
    </div>
</template>