<script>
  export let fetchURL;
  export let articleID;

  console.log('fetchURL =>', fetchURL);
  console.log('Requested article ID =>', articleID);
  const asyncFetch = async() => {
    const response = await fetch(`${fetchURL}`);
    const returnable = await response.json();
    console.log(returnable);
    return returnable
  };
</script>

<section>
  {#await asyncFetch()}
  <p>Loading...</p>
  {:then responseObj}
  <article>
    <h1 class="title">{responseObj.article.title}</h1>
    <span class="subtitle">{responseObj.article.content}</span>
  </article>
  {:catch err}
  <p>Uh-oh: {err}</p>
  {/await}
</section>
