<template>
    <div class="container mt-5">
        <form @submit.prevent="submitForm">
            <div class="field">
                <label class="label">Title</label>
                <div class="control">
                    <input v-model="post.title" class="input" type="text" placeholder="Title">
                </div>
                </div>
                <div class="field">
                <label class="label">Creator</label>
                <div class="control">
                    <input  v-model="post.creator" class="input" type="text" placeholder="Creator">
                </div>
                </div>

                <div class="field">
                <label class="label">Post icerigi</label>
                <div class="control">
                    <textarea  v-model="post.content" class="textarea" placeholder="..."></textarea>
                </div>
                </div>

                <div class="field is-grouped">
                <div class="control">
                    <button type="submit" class="button is-primary">Submit</button>
                </div>
                </div>
        </form> 

    </div>
</template>

<script>
import { inject } from 'vue';

export default {
  setup() {
    const post = inject('post');
    const submitForm = inject('submitForm');
    // post ve submitForm verilerini kullanabilirsiniz

    return {
      post,
      submitForm
    };
  }
}
</script>

<style>

</style>