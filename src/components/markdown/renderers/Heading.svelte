<script>
  import { getContext } from "svelte";
  import { key } from "../context";
  export let depth;
  export let raw;
  export let text;
  export let theme;

  const { slug, getOptions } = getContext(key);
  const options = getOptions();

  $: id = options.headerIds ? options.headerPrefix + slug(text) : undefined;
</script>

{#if depth === 1}
  <h1 class={theme} {id}><slot /></h1>
{:else if depth === 2}
  <h2 class={theme} {id}><slot /></h2>
{:else if depth === 3}
  <h3 class={theme} {id}><slot /></h3>
{:else if depth === 4}
  <h4 class={theme} {id}><slot /></h4>
{:else if depth === 5}
  <h5 class={theme} {id}><slot /></h5>
{:else if depth === 6}
  <h6 class={theme} {id}><slot /></h6>
{:else}
  {raw}
{/if}

<style lang="scss">
  @import "../../../styles/variables.scss";

  h1,h2,h3,h4,h5,h6 {
    text-transform: uppercase;
    font-weight: 600;
  }

  h1 {
    font-size: 1.6rem;
    margin-bottom: 0.8rem;

    &::first-letter {
      color: #000000;
      font-size: 2.4rem;
    }
  }

  h2,h3,h4,h5,h6 {
    margin-bottom: .4rem;

    &::first-letter {
      font-size: 120%;
    }
  }

  h2,h3,h4 {
    font-size: 1.2rem;
  }

  h1.code,
  h2.code,
  h3.code,
  h4.code,
  h5.code,
  h6.code {
    &::first-letter {
      color: $color-blue;
    }
  }

  h1.life,
  h2.life,
  h3.life,
  h4.life,
  h5.life,
  h6.life {
    &::first-letter {
      color: $color-yellow;
    }
  }

  h1.fun,
  h2.fun,
  h3.fun,
  h4.fun,
  h5.fun,
  h6.fun {
    &::first-letter {
      color: $color-red;
    }
  }
</style>
