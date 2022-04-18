<script>
  import { supressWarnings } from './supress-warnings'

  export let type = undefined
  export let tokens = undefined
  export let header = undefined
  export let rows = undefined
  export let ordered = false
  export let renderers
  export let theme

  supressWarnings();
</script>

{#if !type}
  {#each tokens as token}
    <svelte:self {...token} {renderers} {theme} />
  {/each}
{:else}
  {#if renderers[type]}
    {#if type === 'table'}
      <svelte:component this={renderers.table}>
        <svelte:component this={renderers.tablehead} {theme}>
          <svelte:component this={renderers.tablerow} header={true} {theme}>
            {#each header as headerItem, i}
              <svelte:component
                this={renderers.tablecell}
                header={true}
                align={$$restProps.align[i] || 'left'}
                {theme}
                >
                <svelte:self tokens={headerItem.tokens} {renderers} {theme} />
              </svelte:component>
            {/each}
          </svelte:component>
        </svelte:component>
        <svelte:component this={renderers.tablebody}>
          {#each rows as row}
            <svelte:component this={renderers.tablerow} header={false} {theme}>
              {#each row as cells, i}
                <svelte:component
                  this={renderers.tablecell}
                  header={false}
                  align={$$restProps.align[i] || 'left'}
                  {theme}
                  >
                  <svelte:self tokens={cells.tokens} {renderers} {theme} />
                </svelte:component>
              {/each}
            </svelte:component>
          {/each}
        </svelte:component>
      </svelte:component>
    {:else if type === 'list'}
      {#if ordered}
        <svelte:component this={renderers.list} {ordered} {...$$restProps}>
          {#each $$restProps.items as item}
            <svelte:component this={renderers.orderedlistitem || renderers.listitem} {ordered} {theme} {...item}>
              <svelte:self tokens={item.tokens} {renderers} {theme} />
            </svelte:component>
          {/each}
        </svelte:component>
      {:else}
        <svelte:component this={renderers.list} {ordered} {...$$restProps}>
          {#each $$restProps.items as item}
            <svelte:component this={renderers.unorderedlistitem || renderers.listitem} {ordered} {theme} {...item}>
              <svelte:self tokens={item.tokens} {renderers} {theme} />
            </svelte:component>
          {/each}
        </svelte:component>
      {/if}
    {:else}
      <svelte:component this={renderers[type]} {...$$restProps} {theme}>
        {#if tokens}
          <svelte:self {tokens} {renderers} {theme} />
        {:else}
          {$$restProps.raw}
        {/if}
      </svelte:component>
    {/if}
  {/if}
{/if}
