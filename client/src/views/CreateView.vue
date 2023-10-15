<template>
<PostForm/>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import { reactive,provide } from 'vue';
import { useRouter } from "vue-router"

export default {
    components: {
      PostForm
   },
//    props: {
//     post: Object,
//     submitForm: Function,
//   },
   setup() {
      const API_URL = "http://localhost:5000/posts"
      const router = useRouter()

//------------Create---------------
      const post = reactive({
         title: "",
         content: "",
         creator:""
      })

      async function submitForm() {
         const response = await fetch(API_URL, {
            method: "POST",
            headers: {
               "content-type":"application/json"
            },
            body: JSON.stringify({
               title: post.title,
               content: post.content,
               creator:post.creator
            })
         })
         await response.json()
         router.push({
            name:"home"
         })
      }
      //------------Create end---------------
            //------------props gecme--------------
                provide('post', post);
                provide('submitForm', submitForm);
            //------------props gecme---------------

      return {
         post,
         submitForm,
      }
   }
}
</script>

<style>

</style>