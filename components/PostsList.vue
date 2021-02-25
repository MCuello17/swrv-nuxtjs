<template>
  <article>
    <p>
      <strong>
        {{ posts.length }}
      </strong>
      results:
    </p>
    <loading-alert v-if="!posts" class="max-w-screen-xl text-xl mx-auto my-20 flex items-center justify-center" />
    <posts-list-cards v-else :posts="posts || []" />
  </article>
</template>

<script>
import LoadingAlert from './LoadingAlert'
import PostsListCards from './PostsListCards'
export default {
  components: { LoadingAlert, PostsListCards },
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>
