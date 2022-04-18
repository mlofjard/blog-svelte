<script lang="ts">
    import ArticleComponent from "../Article.svelte";
    import type { Article } from "../../../types/articles";

    export let article: Article;
</script>

<ArticleComponent item={article} />

