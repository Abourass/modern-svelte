<script>
  export let content;
  export let articleTitle;
</script>

<section>
  <article>
    <h1 class="title">{articleTitle}</h1>
    <div id="contentArea">{@html content}</div>
  </article>
</section>
