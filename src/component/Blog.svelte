<script>
  export let title;
  export let image;
  export let allHyperlinks;
  export let imageId;

  function showImage(arr, id) {
    for (let i = 0; i < arr.length; i++) {
      if (arr[i].id === id) {
        return arr[i].url;
      }
    }
  }
  let img = showImage(image, imageId.fields.images.sys.id);
  const imageUrl = img;
</script>

<article>
  <h1>{title}</h1>
  <p>
    <!-- hyperlink -->
    {#each allHyperlinks as hlink, i}
      {#each hlink.content as paragraph, i}
        {#if paragraph.nodeType === "hyperlink"}
          {#each paragraph.content as uriLink}
            <a href={paragraph.data.uri}>{uriLink.value}</a>
          {/each}
        {/if}

        <!-- typography -->
        {#if paragraph.nodeType === "text" && paragraph.marks.length === 0}
          {paragraph.value}
        {:else if paragraph.marks?.length > 0}
          {#each paragraph.marks as typo}
            {#if typo.type === "italic"}
              <i>{paragraph.value}</i>
            {:else if typo.type === "bold"}
              <b>{paragraph.value}</b>
            {:else if typo.type === "underline"}
              <u>{paragraph.value}</u>
            {/if}
          {/each}
        {/if}

        <!-- list_item -->
        {#if paragraph.nodeType === "list-item"}
          {#each paragraph.content as list}
            {#each list.content as listed_item}
              <li>{listed_item.value}</li>
            {/each}
          {/each}
        {/if}
      {/each}{/each}
  </p>

  <!-- image -->
  <div><img src={imageUrl} alt={title} /></div>
</article>

<style>
  img {
    width: 900px;
    display: block;
    margin: 0 auto;
    border-radius: 4px;
  }
</style>
