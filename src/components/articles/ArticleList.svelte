<script>
  export let fetchURL;
  export let polarity;
  import Article from './Article.svelte'

  const fetchArticles = async() => {
    const response = await fetch(`${fetchURL}`, {method: 'POST'});
    return await response.json();
  };
</script>

<section class="section">
  {#await fetchArticles()}
    <p>I am currently running this on a free heroku cluster, so sometimes I have to boot the cluster. Give me just a second! Loading...</p>
  {:then articles}
    <Article content="{articles[0].content}" articleTitle="{articles[0].title}" polarity="{polarity}"/>
  {:catch error}
    <p>Seems I can't get my heroku cluster to run. If you wouldn't mind, I'd really appreciate you emailing me about this: xorakjoken7@gmail.com</p>
  {/await}
</section>

<style>
  .section {
    padding: 1rem;
    margin-top: .5rem;
  }
</style>
