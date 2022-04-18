<script>
  export let ordered
  export let start
</script>

{#if ordered}
  <ol {start}><slot></slot></ol>
{:else}
  <ul><slot></slot></ul>
{/if}

<style lang="scss">
  ol, ul {
    margin: 0 0 .8rem 2.4rem;
  }

  ul {
    list-style-type: none;
  }

  ol { 
    list-style-type: decimal;
  }
</style>
