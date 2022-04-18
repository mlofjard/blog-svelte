<script lang="ts">
    import type { ArticleList } from "types/articles";
    import Article from "./Article.svelte";

    export let articles: ArticleList = {
        offset: 0,
        total_rows: 0,
        rows: [],
    };
</script>

<section class="article-list">
    {#each articles.rows as item, i}
        <Article item={item} titleLink={true} />
    {/each}
</section>

<style lang="scss">
    section.article-list {
        max-width: 80rem;
        min-width: 200px;
        display: grid;
        grid-template-columns: auto;
        margin: 0 auto;
        padding: 0;
        gap: 4rem;
    }
</style>
