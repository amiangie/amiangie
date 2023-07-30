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
    <section class="Home js-section" id="Home">
      <h1 class="Home__hero">
        Hi! I'm Angie, and I'm a
        <span>front-end developer</span>
      </h1>
      <p class="Home__note">
        I <a href="#Portfolio">create</a> beautiful and accessible websites, <a href="#random-bits">write</a> about web, and <a href="#Art">paint</a> things.
      </p>
    </section>
    <section class="PageSection About js-section" id="About">
      <ContentRenderer :value="about" />
    </section>
    <section class="PageSection Portfolio js-section" id="Portfolio">
      <ContentRenderer :value="portfolio" />
    </section>
    <section class="PageSection Art js-section" id="Art">
      <img src="amiangie-art.jpg" alt="A painting in style of Leyendecker, featuring players from OG Esports team, four of whom are arranged in front of Aegis, and the oldest one is slumping in a chair, daydreaming about their future wins.">
      <p>Art portfolio is in the works, but here's a sneak peek. Commissions open!</p>
    </section>
    <section class="PageSection Contact js-section" id="Contact">
      <ContentRenderer :value="contact" />
    </section>
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
    background: black;
    font-size: var(--font-size-s);
    padding: var(--indent-nice);
  }

  .PageMain {
    min-height: 100vh;
    padding: 0 var(--indent-nice);
    background: linear-gradient(0deg, rgba(0,0,0,0.8) 35%, rgba(255,255,255,0) 100%);
  }

  .PageSection {
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
        margin: 0;
        padding-bottom: var(--indent-nice);
      }
  }

  .About {
    p:first-child {
      font-size: var(--font-size-l);
      margin-bottom: 3.5em;

      &:before {
        content: 'TL;DR: ';
        display: block;
        margin: 0;
      }
    }
  }

  .Portfolio {
    a {
      font-size: var(--font-size-l);

      &:after {
        content: "";
        display: block;
      }
    }

    li {
      margin-top: 2em;
    }
  }

  .Contact {
    font-size: var(--font-size-l);

    li {
      margin-bottom: 1.5em;
    }
  }

  .Art {
    font-size: 0.75em;
  }

  @media only screen and (min-width: 800px) {
    .PageNav {
      display: flex;

      &__link {
        margin-right: 1ch;

        &:after {
          content: '/';
          margin-left: 1ch;
        }

        &:last-child {
          margin-right: 0;

          &:after {
            display: none;
          }
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

  @media only screen and (min-width: 1280px) {
    .PageHeader {
      background: transparent;
    }

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
</style>