<script>
  export let header;
  export let align;
  export let theme;
</script>

{#if header}
  <th class={theme} {align}><slot /></th>
{:else}
  <td class={theme} {align}><slot /></td>
{/if}

<style lang="scss">
  @import "../../../styles/variables.scss";

  th {
    padding: 0.8rem 1.6rem;

    &:first-of-type {
      border-top-left-radius: 0.8rem;
    }

    &:last-of-type {
      border-top-right-radius: 0.8rem;
    }
  }

  td {
    padding: 0.8rem 1.6rem;
  }
</style>
