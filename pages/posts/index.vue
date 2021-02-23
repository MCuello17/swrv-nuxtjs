<template>
  <section>
    <h1 class="text-2xl font-bold">
      Posts
    </h1>
    <div v-if="error">
      failed to load
    </div>
    <input name="search" type="text" placeholder="Search a post" @keyup="debounceSearch">
    <article v-if="!error">
      <div v-if="!data">
        loading...
      </div>
      <div v-else class="flex flex-wrap justify-center">
        <nuxt-link v-for="post in data" :key="post.id" :to="{name: 'posts-id', params: { id: post.id }}" class="p-4 xl:w-1/4 md:w-1/2 w-7/12 mb-12">
          <div>
            <h3 class="text-lg font-bold">
              {{ post.title }}
            </h3>
            <p>
              {{ post.body }}
            </p>
          </div>
        </nuxt-link>
      </div>
    </article>
  </section>
</template>

<script>
import useSWRV from 'swrv'

async function fetcher (url) {
  const data = await fetch(url)
    .then(response => response.json())
    .then((response) => {
      if (!response.length) { throw new Error('Something went wrong') }
      return response
    })
  return data
}

export default {
  setup (props, { root }) {
    const { data, error, mutate: mutatePosts } = useSWRV(
      () => {
        const search = root.$store.state.search
        const url = 'https://jsonplaceholder.typicode.com/posts' + (search ? `?userId=${search}` : '')
        return url
      },
      fetcher,
      {
        errorRetryInterval: 10000
      }
    )

    function filterPosts () {
      mutatePosts()
    }

    return {
      data,
      error,
      filterPosts
    }
  },
  data () {
    return {
    }
  },
  methods: {
    debounceSearch (e) {
      setTimeout(() => {
        if (this.$store.state.search === e.target.value) { return }
        this.$store.commit('setSearchValue', e.target.value)
        this.filterPosts()
      }, 1000)
    }
  }
}
</script>

<style>

</style>
