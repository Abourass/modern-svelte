<script>
  import 'bulma/css/bulma.css'
  import '@fortawesome/fontawesome-free/css/all.css'
  import { slide } from 'svelte/transition'
  export let title;

  const types = ['is-primary', 'is-success', 'is-danger', 'is-warning', 'is-info', 'is-link', 'is-dark'];
  let type = 'is-primary';
  let lastType = '';

  async function update() {
    lastType = type; type = '';
    setTimeout(() => {
      let key = Math.floor(Math.random() * types.length);
      if (types[key] === lastType){
        key += 1;
        if (key === -1 || key >= types.length){
          key = 3;
        }
      }
      type = types[key];
      }, 1000)
  }
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

  <nav class="navbar is-transparent" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>

    <div id="navbarBasicExample" class="navbar-menu">
      <div class="navbar-start">
        <a class="navbar-item"> Home </a>
        <a class="navbar-item"> Articles </a>
        <a class="navbar-item"> Chatroom </a>
        <div class="navbar-item has-dropdown is-hoverable">
          <a class="navbar-link"> More </a>
          <div class="navbar-dropdown">
            <a class="navbar-item"> Gastronomy </a>
            <a class="navbar-item"> About Me </a>
            <hr class="navbar-divider">
            <a class="navbar-item"> Consulting </a>
          </div>
        </div>
      </div>

      <div class="navbar-end">
        <div class="navbar-item">
          <div class="buttons">
            {#if type}<a class="button {type}" on:click={update}> Change Colors </a>{/if}
          </div>
        </div>
      </div>
    </div>
  </nav>
</main>

<style>
  @import url('https://fonts.googleapis.com/css?family=Poiret+One&display=swap');
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  .title{
    font-family: 'Poiret One', cursive;
  }

</style>
