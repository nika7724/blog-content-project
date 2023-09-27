<script>
  import { onMount } from "svelte";
  import Blog from "./Blog.svelte";
  const space = "u6uvswtswt0w";
  const token = "op_g9tDEMCcJl-NkDpfDOejOkJ4LDvrfo-yAqWqYF4Y";
  const url = `https://cdn.contentful.com/spaces/${space}/environments/master/entries?access_token=${token}`;
  let posts = [];
  let assets = [];

  onMount(async () => {
    const response = await fetch(url);
    const res = await response.json();
    posts = res.items;
    assets = res.includes.Asset.map((a) => {
      return {
        id: a.sys.id,
        url: a.fields.file.url,
      };
    });

    console.log(assets);
    console.log(res);
  });
</script>

{#if posts}
  {#each posts as post, i}
    <Blog
      title={post.fields.title}
      image={assets}
      allHyperlinks={post.fields.richText.content}
      imageId={post}
    />
  {/each}
{/if}
