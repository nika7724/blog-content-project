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
    <h1>{title}</h1>

    <!-- image -->
    <div><img src={imageUrl} alt={title} /></div>
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
    width: 900px;
    display: block;
    margin: 0 auto;
    background-color: #ffffff;
    padding-left: 5%;
    padding-right: 5%;
  }
  img {
    width: 900px;
    display: block;
    margin: 0 auto;
    border-radius: 4px;
    padding-top: 3%;
    padding-bottom: 5%;
  }

  p {
    font-family: "Open Sans", sans-serif;
  }
</style>
