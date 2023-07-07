<script context="module" lang="ts">
   import { navigate } from "svelte-navigator";

   export interface ArticleEdit {
      theme: string;
      title: string;
      htmlContent: string;
   }
</script>

<script lang="ts">
   import { getDateTimeNow } from "../../utils";
   import type { Article } from "../../../types/articles";

   export let article: Article;

   const updateTime = () => {
      article.value.dateTime = getDateTimeNow();
   };

   function uuidv4() {
      return (<any>[1e7] + -1e3 + -4e3 + -8e3 + -1e11).replace(/[018]/g, c =>
         (c ^ (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))).toString(16)
      );
   }

   const savePost = async () => {
      const url = `/api/blog/${article.value._id || uuidv4()}`;
      const res = await fetch(url, {
         method: "PUT",
         credentials: "same-origin", // include, *same-origin, omit
         headers: {
            "Content-Type": "application/json",
         },
         redirect: "follow", // manual, *follow, error
         referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
         body: JSON.stringify(article.value),
      });
      if (res.ok) {
         const val = await res.json();
         article.value._rev = val.rev;
         alert(JSON.stringify(val));
         navigate(`/admin/post/${val.id}`, { replace: true });
      }
   };

   const setReadableKey = (title: string) => {
      let val = title.toLowerCase();
      val = val.replace(/[^a-z0-9]/g, "-");
      article.value.readableKey = val;
   };

   $: setReadableKey(article.value.title);
</script>

<div class="vflex">
   <div class="hflex">
      <button class="save-button" on:click={savePost} />
      <div>
         <input type="text" bind:value={article.value.dateTime} />
         <button class="refresh-time-button" on:click={updateTime} />
      </div>
      <label><input type="checkbox" bind:checked={article.value.published} /> Published</label>
   </div>
   <div class="hflex">
      <select bind:value={article.value.theme}>
         <option>code</option>
         <option>life</option>
         <option>fun</option>
      </select>
      <input type="text" bind:value={article.value.title} />
      <input type="text" bind:value={article.value.author} />
      <input type="text" bind:value={article.value.readableKey} />
   </div>
   <div class="grow">
      <textarea bind:value={article.value.htmlContent} />
   </div>
</div>

<style lang="scss">
   .vflex {
      display: flex;
      flex-direction: column;
      height: 100%;
      width: 100%;
      flex-wrap: wrap;
   }

   .hflex {
      margin: 0.8rem;
      display: flex;
      flex-direction: row;
      align-items: center;
      gap: 0.8rem;

      flex-wrap: wrap;
      width: calc(100% - 1.6rem);
   }

   .grow {
      flex: 1;
   }

   textarea {
      width: calc(100% - 6px);
      height: calc(100% - 8px);
      resize: none;
   }

   input[type="text"],
   select {
      font-size: 0.8rem;
      margin: 0;
      padding: 0.4rem 0.2rem;
   }

   .save-button {
      padding: 0.2rem;

      &::before {
         font-size: 1.6rem;
         font-family: "Material Symbols Rounded";
         content: "\f09b";
      }
   }

   .refresh-time-button {
      padding: 0.2rem;

      &::before {
         font-size: 1rem;
         font-family: "Elusive-Icons";
         content: "\f1da";
      }
   }
</style>
