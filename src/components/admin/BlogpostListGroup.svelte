<script lang="ts">
    import { link } from "svelte-navigator";

    interface Group {
        name: string;
        posts: {
            draft: boolean;
            dateTime: string;
            key: string;
            title: string;
        }[];
    }

    export let group: Group;

    let expanded = group.name === "Drafts" ? true : false;

    const toggle = () => {
        expanded = !expanded;
    };

    $: listStyles = expanded ? "postlist expanded" : "postlist";
    $: headerStyles = expanded ? "header expanded" : "header";
</script>

<div class="group">
    <div class={headerStyles} on:click={toggle}>
        <div class="name">{group.name}</div>
    </div>
    <div class={listStyles}>
        {#each group.posts as post}
            <div class="post">
                <a href="/admin/post/{post.key}" use:link>{post.title}</a>
            </div>
        {/each}
    </div>
</div>

<style lang="scss">
    .group {
        border: 1px solid #000;
        border-bottom: none;

        &:last-of-type {
            border-bottom: 1px solid #000;
        }
    }

    .header {
        display: flex;
        flex-direction: row;
        justify-content: space-between;

        padding: 0.8rem;

        &::after {
            display: block;
            font-family: "Elusive-Icons";
            content: "\f12d";
        }

        &.expanded {
            &::after {
                font-family: "Elusive-Icons";
                display: block;
                content: "\f130";
            }
        }
    }

    .postlist {
        display: none;
        padding-bottom: 1.6rem;

        &.expanded {
            display: block;
        }
    }
    .post {
        padding: 0.4rem 1.6rem;
        text-overflow: ellipsis;
        white-space: nowrap;
        overflow: hidden;
    }
</style>
