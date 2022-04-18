<script lang="ts">
    import ArticleComponent from "../components//Article.svelte";
    import type { Article, ArticleDoc } from "../../types/articles";
    import ResizePane from "../components/admin/ResizePane.svelte";
    import BlogpostEditor from "../components/admin/BlogpostEditor.svelte";
    import BlogpostList from "../components/admin/BlogpostList.svelte";

    export let key: string;

    let article: Article = {
        id: "",
        key: "",
        value: {
            _id: "",
            _rev: "",
            author: "",
            dateTime: "",
            htmlContent: "",
            pictureAltText: "",
            pictureSubText: "",
            pictureURL: "",
            published: false,
            readableKey: "",
            tags: [],
            theme: "code",
            title: "",
            type: "blogpost",
        },
    };

    const baseUrl = "/api/blog/";

    const fetchData = async (keyParam: string) => {
        const fetchUrl = `${baseUrl}${keyParam}`;
        const res = await fetch(fetchUrl);
        article = {
            id: "",
            key: "",
            value: (await res.json()) as ArticleDoc,
        };
    };

    $: fetchData(key);
</script>

<ResizePane leftWidth={300} middleWidth={600}>
    <section slot="left" class="flex">
        <BlogpostList />
    </section>
    <section slot="middle" class="flex">
        <BlogpostEditor bind:article />
    </section>
    <section slot="right" class="flex preview">
        <ArticleComponent item={article} />
    </section>
</ResizePane>

<style lang="scss">
    .flex {
        flex: 1;
        width: calc(100% - 8px);
        overflow: auto;
    }

    .preview {
        padding: 1.6rem;
    }
</style>
