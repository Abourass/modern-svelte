<script>
  export let content;
  export let articleTitle;
  export let polarity;
</script>

  <article>
    <h1 class="title is-{polarity}">{articleTitle}</h1>
    <div id="contentArea" class="content-is-{polarity}">{@html content}</div>
  </article>
