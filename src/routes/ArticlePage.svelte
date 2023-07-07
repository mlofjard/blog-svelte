<script lang="ts">
    import ArticleComponent from "../components/Article.svelte";
    import CommentList from "../components/CommentList.svelte";
    import type {
        ArticleWithComments,
        Article,
        Comment,
    } from "../../types/articles";
    export let key: string;

    let article: Article | undefined = undefined;
    let comments: Comment[] = [];

    const baseUrl = "/api/blog/_design/posts/_view/";

    const fetchData = async (keyParam: string) => {
        const startKey = encodeURIComponent(JSON.stringify([keyParam]));
        const endKey = encodeURIComponent(JSON.stringify([keyParam, 2]));
        const fetchUrl = `${baseUrl}byReadableKeyWithComments?startkey=${startKey}&endkey=${endKey}`;
        const res = await fetch(fetchUrl);
        const fetchedArticle = (await res.json()) as ArticleWithComments;
        console.log(fetchedArticle.rows[0]);
        article = fetchedArticle.rows[0];
        comments = fetchedArticle.rows.slice(1) as Comment[];
    };

    $: fetchData(key);
</script>

{#if article}
    <div class="container">
        <ArticleComponent item={article} />
        <CommentList {comments} theme={article.value.theme} />
    </div>
{/if}

<style lang="scss">
    .container {
        max-width: 120rem;
        min-width: 200px;
        display: flex;
        flex-direction: column;
        margin: 0 auto;
        padding: 0;
        gap: 4rem;
        container-type: inline-size;
    }
</style>
