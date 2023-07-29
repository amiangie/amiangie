<template>
  <header class="PageHeader">
    <NuxtLink :to="{path: '/', hash: '#Home'}" class="Pseudologo">
      Angie's Homepage
    </NuxtLink>

    <nav>
      <ul class="PageNav">
        <li v-for="navItem in navigation" :key="navItem.title" class="PageNav__link">
          <NuxtLink :to="{path: '/', hash: `#${navItem.title}`}">
            {{ navItem.title }}
          </NuxtLink>
        </li>
      </ul>
    </nav>
  </header>
  <main class="PageMain">
    <section class="PageSection Home" id="Home">
      <h1 class="Home__hero">
        Hi! I'm Angie, and I'm a
        <span>front-end developer</span>
      </h1>
      <p class="Home__note">
        I <NuxtLink :to="{path: '/', hash: '#Portfolio'}">create</NuxtLink> beautiful and accessible websites, <a href="https://dev.to/amiangie" target="_blank">write</a> about web, and paint things.
      </p>
    </section>
    <div class="">
    <section class="PageSection About" id="About">
      <ContentRenderer :value="about" />
    </section>
    <section class="PageSection HomPortfolioe" id="Portfolio">
      <ContentRenderer :value="portfolio" />
    </section>
    <section class="PageSection Contact" id="Contact">
      <ContentRenderer :value="contact" />
    </section>
    </div>
  </main>
</template>

<script setup>
const { data: navigation } = await useAsyncData('navigation', () => fetchContentNavigation());

const { data: about } = await useAsyncData('about', () => queryContent('/about').findOne());
const { data: portfolio } = await useAsyncData('portfolio', () => queryContent('/portfolio').findOne());
const { data: contact } = await useAsyncData('contact', () => queryContent('/contact').findOne());
</script>

<style lang="scss">
  .PageHeader {
    position: fixed;
    width: 100%;
    display: flex;
    justify-content: space-between;
    font-size: var(--font-size-s);
    padding: var(--indent-nice);
  }

  .PageMain {
    min-height: 100vh;
    padding: 0 var(--indent-nice);
    background: linear-gradient(0deg, rgba(0,0,0,0.8) 35%, rgba(255,255,255,0) 100%);
  }

  .PageSection {
    display: flex;
    flex-direction: column;
    justify-content: center;
    max-width: 860px;
    margin: 0 auto;
  }

  .Pseudologo {
    text-decoration: none;
  }

  .PageNav {
    display: flex;

    &__link {
      margin-right: 1ch;

      &:not(:last-child):after {
        content: '/';
        margin-left: 1ch;
      }
    }
  }

  .Home {
    display: grid;
    max-width: 100%;
    min-height: 100vh;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 0;
    grid-template-areas: 
      ". . ."
      "main main main"
      ". . note";

      &__hero {
        grid-area: main;
        align-self: center;
        font-size: var(--font-size-l);
        text-align: center;
        line-height: 1;

        span {
          display: block;
          text-transform: uppercase;
          font-size: 8vw;
        }
      }

      &__note {
        grid-area: note;
        align-self: end;
        justify-self: end;
        text-align: right;
        max-width: 30ch;
      }
  }
</style>