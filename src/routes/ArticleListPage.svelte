<script lang="ts">
   export let type: "all" | "code" | "life" | "fun" = "all";
   export let key: string;

   import type { ArticleList } from "types/articles";
   import ArticleListComponent from "../components/ArticleList.svelte";
   import Pager from "../components/Pager.svelte";

   let articles: ArticleList = {
      offset: 0,
      total_rows: 0,
      rows: [],
   };
   let nextKey: string;
   let prevKey: string;

   const baseUrl = "/api/blog/_design/posts/_view/";
   const pageSize = 6;

   const fetchData = async (typeParam: string, keyParam: string) => {
      nextKey = "";
      prevKey = "";
      let firstPage = true;
      let desc = true;
      let restKey: string = "";
      if (keyParam) {
         firstPage = false;
         const prefix = keyParam.substring(0, 1);
         restKey = keyParam.substring(1);
         desc = prefix === "n";
      }
      const allStartKey = encodeURIComponent(JSON.stringify(restKey));
      const topicStartKey = encodeURIComponent(JSON.stringify(keyParam ? [typeParam, desc ? 0 : 0, restKey] : [typeParam, desc ? 1 : 0]));
      const topicEndKey = encodeURIComponent(JSON.stringify([typeParam, desc ? -1 : 1]));
      const keys = type === "all" ? (keyParam ? `&startkey=${allStartKey}` : "") : `&startkey=${topicStartKey}&endkey=${topicEndKey}`;
      const fetchUrl = `${baseUrl}${type === "all" ? "byDateTime" : "byThemeAndDateTime"}?descending=${desc}&limit=${
         desc ? pageSize : pageSize + 1
      }${keys}`;

      const res = await fetch(fetchUrl);
      const fetchedArticles = (await res.json()) as ArticleList;

      if (!desc) {
         if (fetchedArticles.rows.length < pageSize + 1) {
            firstPage = true;
         } else {
            fetchedArticles.rows.pop();
         }

         // reverse doc if we came from a "prev page" click
         // since we then selected with descending: false;
         fetchedArticles.rows.reverse();
      }

      if (fetchedArticles.rows.length == pageSize) {
         nextKey = (typeParam === "all" ? fetchedArticles.rows.pop()?.key : fetchedArticles.rows.pop()?.key[2]) || "";
      }

      if (fetchedArticles.rows.length > 0 && !firstPage) {
         prevKey = typeParam === "all" ? fetchedArticles.rows[0].key : fetchedArticles.rows[0].key[2];
      }

      articles = {
         offset: 0,
         total_rows: 0,
         rows: fetchedArticles.rows,
      };
   };

   $: fetchData(type, key);
</script>

<section class="article-list">
   <ArticleListComponent {articles} />
</section>
<Pager
   firstPage={!!!prevKey}
   lastPage={!!!nextKey}
   nextUrl="/topic/{type}/n{nextKey}"
   nextTitle="Older posts"
   prevUrl="/topic/{type}/p{prevKey}"
   prevTitle="Newer posts"
/>

<style lang="scss">
   section.article-list {
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
