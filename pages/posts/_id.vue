<template>
  <section>
    <error-modal v-if="error" @close-modal="error = false" />
    <post-body v-if="!error" :post="post || {}" />
  </section>
</template>

<script>
import useSWRV from 'swrv'
import PostBody from '../../components/PostBody'

async function fetcher (url) {
  const data = await fetch(url)
    .then(response => response.json())
    .then((response) => {
      if (!response[0]) { throw new Error('Post doesn\'t exist') }
      return response[0]
    })

  return data
}

export default {
  components: { PostBody },
  setup (props, { root }) {
    const { data: post, error } = useSWRV(
      () => `https://jsonplaceholder.typicode.com/posts/?id=${root.$route.params.id}`,
      fetcher,
      {
        errorRetryInterval: 10000
      }
    )

    console.log({ post })
    return {
      post,
      error
    }
  }
}
</script>

<style>

</style>
