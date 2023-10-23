<script>
  export let title, image, imageId, selectedChunkOfData;
  let img;

  function showImage(arr, id) {
    for (let i = 0; i < arr.length; i++) {
      if (arr[i].id === id) {
        return arr[i].url;
      }
    }
  }
  img = showImage(image, imageId.fields.images.sys.id);
  const imageUrl = img;
</script>

<body>
  <article>
    <!-- <div class="header">
    <img src 
    </div> -->
    <h3>{title}</h3>

    <!-- image -->
    <div><img src={imageUrl} alt={title} /></div>

    <!-- {#if imageId.fields.images.sys.id.length === " "}
      
    {:else}
      <div><img src={imageUrl} alt={title} /></div>
    {/if} -->

    <p>
      <!-- hyperlink -->
      {#each selectedChunkOfData as contents}
        {#if contents.value_hyperlink?.length >= 0}
          <a href={contents.url}>{contents.value_hyperlink}</a>
        {/if}

        <!-- typography -->
        {#if contents.nodeType === "text" && contents.marks?.length === 0}
          {contents.value}
        {:else if contents.marks?.length > 0}
          {#each contents.marks as typo}
            {#if typo.type === "italic"}
              <i>{contents.value}</i>
            {:else if typo.type === "bold"}
              <b>{contents.value}</b>
            {:else if typo.type === "underline"}
              <u>{contents.value}</u>
            {/if}
          {/each}
        {/if}

        <!-- list_item -->
        {#if contents.list_value}
          <li>{contents.list_value}</li>
        {/if}
      {/each}
    </p>
  </article>
</body>

<style>
  /* body {
    background-color: #f7ddc6;
  } */

  article {
    width: 750px;
    display: block;
    margin: auto;
    background-color: #f7ddc6;
    padding-left: 5%;
    padding-right: 5%;
  }

  img {
    width: 750px;
    height: 400px;
    display: block;
    margin: auto;
    border-radius: 1px;
    padding-top: 1%;
  }

  p {
    font-family: "Open Sans", sans-serif;
    padding-bottom: 6%;
    line-height: 30px;
  }

  h3 {
    font-family: "Open Sans", sans-serif;
    padding-top: 6%;
  }
</style>
