<script>
  export let fetchURL;
  import Article from './Article.svelte'

  console.log('Base FetchURL =>', fetchURL);
  const fetchArticles = async() => {
    const response = await fetch(`${fetchURL}`);
    return await response.json();
  };
</script>

<section class="section">
  {#await fetchArticles()}
    <p>I am currently running this on a free heroku cluster, so sometimes I have to boot the cluster. Give me just a second! Loading...</p>
  {:then articles}
    <Article content="{articles.article.content}" title="{articles.article.title}"/>
  {:catch error}
    <p>Seems I can't get my heroku cluster to run. If you wouldn't mind, I'd really appreciate you emailing me about this: xorakjoken7@gmail.com</p>
  {/await}
</section>
