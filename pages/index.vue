<template>
  <header class="PageHeader">
    <NuxtLink :to="{path: '/', hash: '#Home'}">
      Angie's Homepage
    </NuxtLink>

    <nav>
      <ul class="PageNav">
        <li v-for="navItem in navigation" :key="navItem.title">
          <NuxtLink :to="{path: '/', hash: `#${navItem.title}`}">
            {{ navItem.title }}
          </NuxtLink>
        </li>
      </ul>
    </nav>
  </header>
  <main>
    <section class="PageSection Home" id="Home">
      <h1>
        Hi! I'm Angie, and I'm a
        <span>front-end developer</span>
      </h1>
      <p class="Home__note">
        I <NuxtLink :to="{path: '/', hash: '#Portfolio'}">create</NuxtLink> beautiful and accessible websites, <a href="https://dev.to/amiangie" target="_blank">write</a> about web, and paint things.
      </p>
    </section>
    <section id="About">
      <ContentRenderer :value="about" />
    </section>
    <section id="Portfolio">
      <ContentRenderer :value="portfolio" />
    </section>
    <section id="Contact">
      <ContentRenderer :value="contact" />
    </section>
  </main>
</template>

<script setup>
const { data: navigation } = await useAsyncData('navigation', () => fetchContentNavigation())

const { data: about } = await useAsyncData('about', () => queryContent('/about').findOne())
const { data: portfolio } = await useAsyncData('portfolio', () => queryContent('/portfolio').findOne())
const { data: contact } = await useAsyncData('contact', () => queryContent('/contact').findOne())
</script>

<style lang="scss">
 
</style>