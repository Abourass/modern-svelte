<script>
  import Header from './components/Header.svelte';
  import ArticleList from './components/articles/ArticleList.svelte';

  export let title;
</script>

<main>
  <Header title="{title}" />
  <ArticleList fetchURL="https://the-modern-farm.herokuapp.com/" />
</main>

<style>

</style>
