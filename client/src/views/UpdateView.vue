<template>
    <PostForm/>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import { useRouter, useRoute } from 'vue-router'
import { ref, onMounted,provide } from 'vue'
export default {
    components: {
        PostForm
    },
    setup() {
        const router = useRouter()
        const route = useRoute()

        const API_URL = 'http://localhost:5000/posts'

        const post = ref({
        title: '',
        content: '',
        creator: '',
        })

        onMounted(() => {
            getPost()
        })
          async function getPost() {
            const { id } = route.params
            const response = await fetch(`${API_URL}/${id}`)
             const json = await response.json()
             post.value = json
    }
          async function updatePost() {
                try {
                const { id } = route.params
                const response = await fetch(`${API_URL}/${id}`, {
                method: 'PUT',
                headers: {
                    'content-type': 'application/json',
                },
                body: JSON.stringify({
                    title: post.value.title,
                    content: post.value.content,
                    creator: post.value.creator,
                }),
                })
                await response.json()
                router.push({
                name: 'home',
                })
                }
                catch (error) {
                console.log(error)
                }
        }
     //------------props gecme--------------
                provide('post', post);
                provide('submitForm', updatePost);
    //------------props gecme---------------
    return {
      post,
      updatePost,
    }
    }
}
</script>

<style>

</style>