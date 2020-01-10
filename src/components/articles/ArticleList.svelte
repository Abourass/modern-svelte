<script>
  export let fetchURL;
  import Article from './Article.svelte'
</script>

<section class="section">
  <Article articleID="1" fetchURL="{fetchURL}"/>
</section>
