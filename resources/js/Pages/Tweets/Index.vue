
<template>
    <AppLayout title="Profile">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Les derniers Tweets
            </h2>
        </template>


            <tweet-create></tweet-create>

        <div class="py-12">
            <div class="max-w-3xl mx-auto sm:px-6 lg:px-8">
                <div v-for="tweet in tweets" v-bind:key="tweet.id" class="flex items-center space-x-4 bg-white overflow-hidden rounded
                rounded-b-none border-b-2 border-gray-200 py-6 px-4">
                    <img class="h-16 w-16 object-cover rounded-full" :src="tweet.user.profile_photo_url">
                    <div class="flex flex-col w-2/3">
                    <div>
                        <a class="text-sm text-gray-900 font-bold hover:text-blue-400" :href="`/profile/${tweet.user.name}`">
                            {{ tweet.user.name }}
                        </a>
                        <span class="font-thin text-gray-400">· le {{ tweet.created_at }}</span>
                    </div>
                    <div class="text-sm text-gray-400 font-thin">{{ tweet.content }}</div>
                    </div>
                    <div v-if="tweet.user.id !== $page.props.user.id">
                        <Link v-if="!tweet.user.is_followed" as="button" :href="`/follows/${tweet.user.id}`" method="POST"
                            class="bg-white text-blue-500 cursor-pointer px-5 py-2 hover:text-white border
                            border-blue-500 leading-tight hover:bg-blue-500 rounded-full
                            font-extrabold transition-all duration-300"
                        preserve-scroll>Suivre</Link>

                        <Link v-else as="button" :href="`/unfollows/${tweet.user.id}`" method="POST"
                            class="bg-white text-blue-500 cursor-pointer px-5 py-2 flex-shrink-0
                            hover:text-white border border-blue-500 leading-tight hover:bg-blue-500
                            rounded-full font-extrabold transition-all duration-300" preserve-scroll>Ne Plus Suivre
                         </Link>

                    </div>


                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
import AppLayout from '@/Layouts/AppLayout.vue';
import TweetCreate from '@/Pages/Tweets/Create.vue';
import { Link } from '@inertiajs/vue3';

export default {


    components:{
    AppLayout,
    TweetCreate,
    Link
},

    props:{
        tweets: Array,

    }

}
</script>
