<template>
  <div class="max-w-screen-xl mx-auto text-center">
    <div>
      <h1 class="title block text-bold">
        Welcome!
      </h1>
      <div class="my-20">
        <nuxt-link to="/posts" class="rounded px-4 py-2 font-bold text-white bg-green-500 hover:bg-green-600">
          Click here to get to the post list
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style>
.title {
  font-size: 100px;
}
</style>
