<template>
  <section class="max-w-screen-xl px-4 md:px-12 mx-auto">
    <h1 class="text-2xl font-bold">
      Posts
    </h1>
    <error-modal v-if="error" @close-modal="error = false" />
    <input class="shadow-md rounded-md border border-gray-500 px-4 py-2 w-full md:w-auto mb-12" name="search" type="number" placeholder="Filter by user ID" @input="debounceSearch">
    <posts-list v-if="!error" :posts="posts || {}" />
  </section>
</template>

<script>
import useSWRV from 'swrv'
import ErrorModal from '../../components/ErrorModal'
import PostsList from '../../components/PostsList'

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
  components: { ErrorModal, PostsList },
  setup (props, { root }) {
    const { data: posts, error, mutate: mutatePosts } = useSWRV(
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
      posts,
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
