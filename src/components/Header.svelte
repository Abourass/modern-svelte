<script>
  import 'bulma/css/bulma.css'
  import '@fortawesome/fontawesome-free/css/all.css'
  import { slide } from 'svelte/transition'
  export let title;
  export let type;
</script>

<main>
  {#if type}
    <section class="hero {type}" transition:slide>
      <div class="hero-body">
        <div class="container">
          <h1 class="title">{title}</h1>
        </div>
      </div>
    </section>
  {/if}
</main>

<style>
  main {
    text-align: center;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .title{
    font-family: 'Poiret One', cursive;
    font-size: 4em;
    font-weight: 100;
  }
</style>
