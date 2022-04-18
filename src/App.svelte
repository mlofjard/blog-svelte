<!-- App.svelte -->
<script lang="ts">
  import { Router, Route } from "svelte-navigator";
  import ArticleListPage from "./routes/ArticleListPage.svelte";
  import ArticlePage from "./routes/ArticlePage.svelte";
  import AdminPage from "./routes/AdminPage.svelte";
  import EditorPage from "./routes/EditorPage.svelte";
  import MainLayout from "./components/MainLayout.svelte";
  import AdminLayout from "./components/AdminLayout.svelte";

  type topic = "all" | "code" | "life" | "fun";
  const getTopic = (typeParam: string): topic => {
    if (
      typeParam === "all" ||
      typeParam === "code" ||
      typeParam === "life" ||
      typeParam === "fun"
    ) {
      return typeParam;
    }
    return "all";
  };
</script>

<Router>
  <Route path="/">
    <MainLayout>
      <ArticleListPage type="all" key="" />
    </MainLayout>
  </Route>
  <Route path="/post/:key" let:params>
    <MainLayout>
      <ArticlePage key={params.key} />
    </MainLayout>
  </Route>
  <Route path="/topic/:type" let:params>
    <MainLayout>
      <ArticleListPage type={getTopic(params.type)} key="" />
    </MainLayout>
  </Route>
  <Route path="/topic/:type/:key" let:params>
    <MainLayout>
      <ArticleListPage type={getTopic(params.type)} key={params.key} />
    </MainLayout>
  </Route>
  <Route path="/admin" let:params>
    <AdminLayout>
      <AdminPage />
    </AdminLayout>
  </Route>
  <Route path="/admin/post/:key" let:params>
    <AdminLayout>
      <EditorPage key={params.key} />
    </AdminLayout>
  </Route>
</Router>
