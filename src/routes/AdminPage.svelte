<script lang="ts">
    import ResizePane from "../components/admin/ResizePane.svelte";
    import BlogpostList from "../components/admin/BlogpostList.svelte";
</script>

<ResizePane leftWidth={300} middleWidth={600}>
    <section slot="left" class="flex">
        <BlogpostList />
    </section>
    <section slot="middle" class="flex">Select a post to start editing</section>
    <section slot="right" class="flex">-- Preview --</section>
</ResizePane>

<style lang="scss">
    .flex {
        flex: 1;
        width: calc(100% - 8px);
    }
</style>
