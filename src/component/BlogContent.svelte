<script>
  import { onMount } from "svelte";
  import Blog from "./Blog.svelte";
  const space = "u6uvswtswt0w";
  const token = "op_g9tDEMCcJl-NkDpfDOejOkJ4LDvrfo-yAqWqYF4Y";
  const url = `https://cdn.contentful.com/spaces/${space}/environments/master/entries?access_token=${token}`;
  let posts = [],
    assets = [],
    myNiceStruc = [],
    temp = [],
    details;

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

    for (let i = 0; i < posts.length; i++) {
      posts[i].fields.richText.content.forEach((content) => {
        content.content.forEach((nestedContent) => {
          temp.push({
            value: nestedContent.value,
            nodeType: nestedContent.nodeType,
            marks: nestedContent.marks,
          });
          nestedContent.content?.forEach((nested_Content) => {
            temp.push({
              url: nestedContent.data.uri,
              value_hyperlink: nested_Content.value,
            });
            console.log(nested_Content.value);
            nested_Content.content?.forEach((nest_Content) => {
              temp.push({
                list_value: nest_Content.value,
              });
            });
          });
        });
      });
      myNiceStruc.push(temp);
      temp = [];
    }
    details = myNiceStruc;
  });
</script>

{#if posts}
  {#each posts as post, i}
    <Blog
      title={post.fields.title}
      image={assets}
      imageId={post}
      selectedChunkOfData={details[i]}
    />
  {/each}
{/if}
