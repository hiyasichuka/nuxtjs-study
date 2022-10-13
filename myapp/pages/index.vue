<template>
  <div>
    <nav>
      <ul>
        <li>
          <NuxtLink to="/">Home</NuxtLink>
        </li>
        <li>
          <NuxtLink to="/about">About Page</NuxtLink>
        </li>
      </ul>
    </nav>
    <h1>Hello Nuxters! 👋</h1>
    <p>
      This page is rendered on the <strong>{{ rendering }}</strong>
    </p>
    <p v-if="rendering === 'server'">
      First load or hard refresh is done on server side.
    </p>
    <p v-if="rendering === 'client'">Navigation is done on client side.</p>
    <ul>
      <li>Refresh the page for server side rendering.</li>
      <li>Click the links to see client side rendering.</li>
    </ul>
    <ul v-for="mountain in mountains" :key="mountain.id">
      <NuxtLink :to="`${mountain.continent.toLowerCase()}/${mountain.slug}`">
        <li>{{ mountain.title }}</li>
      </NuxtLink>
    </ul>
    <NuxtLink to="/about">About Page</NuxtLink>
  </div>
</template>
<script>
export default {
  async asyncData() {
    const mountains = await fetch(
        'https://api.nuxtjs.dev/mountains'
      ).then((res) => res.json())

    return {
      rendering: process.server ? 'server' : 'client',
      mountains
    }
  }
}
</script>
