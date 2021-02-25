<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-x-4 gap-y-8 justify-center">
    <nuxt-link v-for="post in posts" :key="post.id" :to="{name: 'posts-id', params: { id: post.id }}" class="p-4 pt-8 rounded-lg shadow-lg hover:shadow-2xl transition duration-500 ease relative overflow-hidden">
      <div class="absolute right-0 top-0 px-2 py-1 text-white bg-green-600 rounded-bl-md">
        user: {{ post.userId }}
      </div>
      <h3 class="text-lg font-bold border border-t-0 border-l-0 border-r-0 border-black border-solid pb-4 mb-4">
        {{ post.title }}
      </h3>
      <p>
        {{ post.body }}
      </p>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  props: {
    posts: {
      type: [Array],
      required: true
    }
  }
}
</script>
