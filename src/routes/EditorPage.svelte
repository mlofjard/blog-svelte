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
      article.value = { ...article.value, ...(await res.json()) as ArticleDoc };
   };

   $: fetchData(key);
</script>

<ResizePane leftWidth={300} middleWidth={600}>
   <section slot="left" class="flex flat-bg">
      <BlogpostList />
   </section>
   <section slot="middle" class="flex flat-bg">
      <BlogpostEditor bind:article />
   </section>
   <section slot="right" class="flex preview blog-bg">
      <ArticleComponent item={article} />
   </section>
</ResizePane>

<style lang="scss">
   .flex {
      flex: 1;
      width: calc(100% - 8px);
      overflow: auto;
   }

   .flat-bg {
      background-color: rgb(80, 80, 80);
   }

   .blog-bg {
      background: radial-gradient(circle at top left, rgba(0, 255, 255, 0.3) 0%, transparent 60%),
         radial-gradient(circle at bottom right, rgba(255, 0, 255, 0.2) 0%, transparent 60%), radial-gradient(circle, #aaa, #222);
   }

   .preview {
      display: flex;
      justify-content: center;
      padding: 1.6rem;
      container-type: inline-size;
   }
</style>
