<template>
  <div>
    <NuxtPage />
  </div>
</template>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Jost&display=swap');

  * {
    box-sizing: border-box;
  }

  html {
    scroll-behavior: smooth;
    font-family: 'Jost', sans-serif;
    font-size: 12px;
    background: url('/amiangie-bg.jpg') center center no-repeat fixed;
    background-size: cover;

    --color-text: #f2bd38;
    --font-size-l: 2.5rem;
    --font-size-m: 1.68rem; 
    --font-size-s: 1.5rem;
    --indent-nice: 34px;
  }

  body {
    color: var(--color-text);
    margin: 0;
    font-size: var(--font-size-m);
    line-height: 1.5;
  }

  a {
    color: unset;
    -webkit-text-underline-position: under;
    text-underline-position: under;

    &:hover {
      text-decoration: none;
    }
  }

  ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
  }

  h2 {
    font-size: var(--font-size-m);
    text-align: center;
    margin-top: 5.5em;

    &:first-child {
      margin-top: 0;
    }
  }

  @media only screen and (min-width: 800px) {
    html {
      font-size: 16px;
      --indent-nice: 69px;
    }
  }
</style>