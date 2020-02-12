<script>
  export let fetchURL;
  export let polarity;
  import Article from './Article.svelte'

  const fetchArticles = async() => {
    const response = await fetch(`${fetchURL}`, {method: 'POST'});
    const responseAsJSON = await response.json();
    return  responseAsJSON
  };
  let articleLoaded = null;
</script>

<section class="section">
  {#await fetchArticles()}
    <p>I am now running this site on a free heroku cluster; as a result when no one's visited the site in an hour or so the cluster shuts down. The cluster is currently booting. Give it just a second! Loading...</p>
  {:then articles}
    {#if articleLoaded}
      <div on:click={()=> articleLoaded = null} class="bk-btn"><div class="bk-btn-triangle"></div><div class="bk-btn-bar"></div></div>
      <Article content="{articles.filter(article => article.number === articleLoaded)[0].content}" articleTitle="{articles.filter(article => article.number === articleLoaded)[0].title}" polarity="{polarity}"/>
    {:else}
      {#each articles as article}
        <div class="container">
          <div class="notification is-transparent" on:click={()=> articleLoaded = article.number}>
            <p class="title is-4">{article.title}</p>
            <p class="subtitle is-6">{article.author}</p>
          </div>
        </div>
      {/each}
    {/if}
  {:catch error}
    <p>Seems I can't get my heroku cluster to run. If you wouldn't mind, I'd really appreciate you emailing me about this: xorakjoken7@gmail.com</p>
  {/await}
</section>

<style>
  .section {
    padding: 1rem;
    margin-top: .5rem;
  }

  .bk-btn {
    height: 52px;
    width: 52px;
    background-color: black;
    border-radius: 50%;
  }
  .bk-btn .bk-btn-triangle {
    position: relative;
    top: 13px;
    left: 10.4px;
    width: 0;
    height: 0;
    border-top: 13px solid transparent;
    border-bottom: 13px solid transparent;
    border-right: 13px solid white;
  }
  .bk-btn .bk-btn-bar {
    position: relative;
    background-color: white;
    height: 7.8px;
    width: 13px;
    top: -3.64px;
    left: 22.88px;
  }
</style>
