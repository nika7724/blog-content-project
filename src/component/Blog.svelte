<script>
  export let title;
  export let image;
  export let alt;
  export let allHyperlinks;
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

        <!-- list_item -->
        {#if paragraph.nodeType === "list-item"}
          <li>{paragraph.value}</li>
        {/if}

        <!-- text_with_typography -->
        <!-- {#if paragraph.nodeType === "text" && paragraph.marks.length === 0}
          {paragraph.value}
        {/if}
        {#if paragraph.marks}
          {#each paragraph.marks as typo}
            {#if typo.type === "italic"}
              <i>{paragraph.value}</i>
            {:else if typo.type === "bold"}
              <b>{paragraph.value}</b>
            {:else if typo.type === "underline"}
              <u>{paragraph.value}</u>
            {/if}
          {/each}
        {/if} -->

        {#if paragraph.nodeType === "text" && paragraph.marks.length === 0}
          {paragraph.value}
        {:else if paragraph.marks?.length > 0}
          {#each paragraph.marks as typo}
            {#if typo.type === "italic"}
              <i>{paragraph.value}</i>
            {:else if typo.type === "bold"}
              <b>{paragraph.value}</b>
            {:else if typo.type === "underline"}
              {paragraph.value}
            {/if}
          {/each}
        {/if}
      {/each}{/each}
  </p>

  <div>
    <img src={image} {alt} />
  </div>

  <!-- <div>
    {#each allImage as imageLink, i}
      {#if imageLink.contentType === "image/jpeg"}
        <img src={imageLink.url} alt={title} />
      {/if}
    {/each}
  </div> -->
</article>
