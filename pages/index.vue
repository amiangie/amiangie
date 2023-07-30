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
    <section class="Home" id="Home">
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
    top: 0;
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
    max-width: 750px;
    margin: 0 auto;
    padding: 150px 0;
  }

  .Pseudologo {
    text-decoration: none;
  }

  .Home {
    display: grid;
    min-height: 100vh;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    gap: 0;
    grid-template-areas: 
      ". . ."
      "main main main"
      ". note note";

      &__hero {
        grid-area: main;
        align-self: center;
        font-size: var(--font-size-s);
        line-height: 1;

        span {
          display: block;
          text-transform: uppercase;
          font-size: 12vw;
        }
      }

      &__note {
        grid-area: note;
        align-self: end;
        justify-self: end;
        text-align: right;
      }
  }

  .About {
    p:first-child {
      font-size: 1.6em;
      margin-bottom: 3.5em;

      &:before {
        content: 'TL;DR: ';
        display: block;
        margin: 0;
      }
    }
  }

  @media only screen and (min-width: 1280px) {
    .About {
      p:first-child {
        &:before {
          content: 'TL;DR: ';
          display: inline;
          margin-left: -5.5ch;
        }
      }
    }
  }

  @media only screen and (min-width: 800px) {
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
      grid-template-areas: 
        ". . ."
        "main main main"
        ". . note";

        &__hero {
          font-size: var(--font-size-l);
          text-align: center;

          span {
            font-size: 8vw;
          }
        }

        &__note {
          max-width: 30ch;
        }
      }
    }
</style>