<script>
  import {onMount} from 'svelte';
  import Header from './components/Header.svelte';
  import ArticleList from './components/articles/ArticleList.svelte';

  const apiURL = 'https://the-modern-farm.herokuapp.com/';
  let data = [];


  export let title;
</script>

<main>
  <Header title="{title}" />
  <ArticleList fetchURL="https://the-modern-farm.herokuapp.com/" />
</main>

<style>

</style>
