<template>
  <nav class="bg-gray-800 fixed w-full z-10">
    <div class="max-w-screen-xl mx-auto px-2 sm:px-6 lg:px-8 py-4 text-white">
      <nuxt-link to="/" class="mx-2 md:mx-8 text-bold relative">
        Home
      </nuxt-link>
      <nuxt-link to="/posts" class="mx-2 md:mx-8 text-bold relative">
        Posts
      </nuxt-link>
    </div>
  </nav>
</template>

<style scoped>
.nuxt-link-exact-active:after {
    content: '';
    font-weight: bold;
    position: absolute;
    bottom: -.5rem;
    left: 50%;
    transform: translateX(-50%);
    height: 2px;
    width: 50%;
    border-radius: 500px;
    --tw-bg-opacity: 1;
    background-color: rgba(5, 150, 105, var(--tw-bg-opacity));
}
</style>
