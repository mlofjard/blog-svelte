<script lang="ts">
    import type {
        AdminBlogpostList,
        AdminBlogpost,
    } from "../../../types/articles";
    import BlogpostListGroup from "./BlogpostListGroup.svelte";

    interface Posts {
        groups: {
            name: string;
            posts: {
                key: string;
                dateTime: string;
                title: string;
                draft: boolean;
            }[];
        }[];
    }

    let renderPosts: Posts = {
        groups: [],
    };

    let blogposts: AdminBlogpostList = {
        offset: 0,
        total_rows: 0,
        rows: [],
    };
    let lastGroup = "";

    const baseUrl = "/api/blog/_design/admin/_view/";

    const fetchData = async () => {
        const fetchUrl = `${baseUrl}byDraftAndDateTime?descending=true`;
        const res = await fetch(fetchUrl);
        blogposts = (await res.json()) as AdminBlogpostList;

        const allPosts: Posts = {
            groups: [
                {
                    name: "Drafts",
                    posts: [],
                },
            ],
        };
        for (const post of blogposts.rows) {
            if (post.key[0]) {
                allPosts.groups[0].posts.push({
                    dateTime: post.key[1],
                    draft: true,
                    key: post.id,
                    title: post.value.title,
                });
            } else {
                const group = getGroup(post);
                if (newGroup(group)) {
                    allPosts.groups.push({ name: group, posts: [] });
                }
                allPosts.groups[allPosts.groups.length - 1].posts.push({
                    dateTime: post.key[1],
                    draft: true,
                    key: post.id,
                    title: post.value.title,
                });
            }
        }
        renderPosts = allPosts;
    };

    const getGroup = (post: AdminBlogpost) => {
        if (post.key[0]) return "draft";
        return new Date(post.key[1]).getFullYear().toString();
    };

    const newGroup = (group: string): boolean => {
        let val = false;
        if (group !== lastGroup) {
            val = true;
        }
        lastGroup = group;
        return val;
    };

    fetchData();
</script>

{#each renderPosts.groups as group}
    <BlogpostListGroup {group} />
{/each}
