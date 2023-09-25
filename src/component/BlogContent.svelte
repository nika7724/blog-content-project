<script>
  import { onMount } from "svelte";
  import Blog from "./Blog.svelte";
  const space = "u6uvswtswt0w";
  const token = "op_g9tDEMCcJl-NkDpfDOejOkJ4LDvrfo-yAqWqYF4Y";
  const url = `https://cdn.contentful.com/spaces/${space}/environments/master/entries?access_token=${token}`;
  let posts = [];

  onMount(async () => {
    const response = await fetch(url)
      .then((response) => response.json()) //json content(promise)
      .then((result) => (posts = result));
    // .catch(function (error) {
    //   console.log(error);
    // });
    console.log(posts);
  });
</script>

{#if posts.items}
  {#each posts.items as _, i}
    <Blog
      title={_.fields.title}
      image={posts.includes["Asset"][0].fields.file.url}
      alt={_.fields.title}
      allHyperlinks={_.fields.richText.content}
    />
  {/each}
{/if}

<!-- 
image={posts.includes["Asset"]} -->
