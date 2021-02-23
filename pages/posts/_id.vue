<template>
  <section>
    <div v-if="error">
      failed to load
    </div>
    <article v-if="!error">
      <div v-if="!data">
        loading...
      </div>
      <div v-else class="">
        <h1 class="text-2xl font-bold">
          {{ data.title }}
        </h1>
        <p>
          {{ data.body }}
        </p>
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
      if (!response[0]) { throw new Error('Post doesn\'t exist') }
      return response[0]
    })

  return data
}

export default {
  setup (props, { root }) {
    const { data, error } = useSWRV(
      () => `https://jsonplaceholder.typicode.com/posts/?id=${root.$route.params.id}`,
      fetcher,
      {
        errorRetryInterval: 10000
      }
    )
    return {
      data,
      error
    }
  }
}
</script>

<style>

</style>
