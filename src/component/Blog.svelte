<script>
  export let title;
  export let image;
  export let alt;
  export let allHyperlinks;
  export let imageItem;
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
  <!-- <div>
    <img src={image} {alt} />
  </div> -->

  {#each image as imageLink, i}
    {#each imageItem as imageTitle}
      {#if imageLink.fields.file.contentType === "image/jpeg" && imageLink.sys.id === imageTitle.fields.images.sys.id}
        <img src={imageLink.fields.file.url} alt={title} />
      {/if}
    {/each}
  {/each}
</article>

<style>
  img {
    width: 900px;
    display: block;
    margin: 0 auto;
    border-radius: 4px;
  }
</style>
