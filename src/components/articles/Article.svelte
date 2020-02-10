<script>
  export let content;
  export let articleTitle;
  export let polarity;
</script>


  <article>
    <h1 class="title is-{polarity}">{articleTitle}</h1>
    <div id="contentArea">{@html content}</div>
  </article>

<style>
  .title.is-dark {
    color: whitesmoke;
  }

  .title.is-grey {
    color: whitesmoke;
  }

  .title.is-light {
    color: #333333;
  }
</style>
