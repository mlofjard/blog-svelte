<script lang="ts">
   import type { ArticleList } from "types/articles";
   import Article from "./Article.svelte";

   export let articles: ArticleList = {
      offset: 0,
      total_rows: 0,
      rows: [],
   };
</script>

{#each articles.rows as item, i}
   <Article {item} titleLink={true} />
{/each}
