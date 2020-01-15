<script>
  import Header from './components/Header.svelte';
  import ArticleList from './components/articles/ArticleList.svelte';

  const apiURL = 'https://the-modern-farm.herokuapp.com/article/all';
  const types = ['is-primary', 'is-success', 'is-danger', 'is-warning', 'is-info', 'is-link', 'is-dark'];
  let data = [], polarity = 'dark', type = 'is-primary', lastType = '';

  const switchPolarity = () => polarity === 'dark' ? polarity = 'light' : polarity = 'dark';
  const switchType = async() => {
    lastType = type; type = '';
    setTimeout(() => {
      let key = Math.floor(Math.random() * types.length);
      if (types[key] === lastType){key += 1; if (key === -1 || key >= types.length){ key = 3; }}
      type = types[key];
    }, 1000)
  };

  document.addEventListener('DOMContentLoaded', () => {
    const $navbarBurgers = Array.prototype.slice.call(document.querySelectorAll('.navbar-burger'), 0); // Get all "navbar-burger" elements
    if ($navbarBurgers.length > 0) { // Check if there are any navbar burgers
      $navbarBurgers.forEach( el => { // Add a click event on each of them
        el.addEventListener('click', () => {
          const target = el.dataset.target; // Get the target from the "data-target" attribute
          const $target = document.getElementById(target);
          el.classList.toggle('is-active'); // Toggle the "is-active" class on both the "navbar-burger" and the "navbar-menu"
          $target.classList.toggle('is-active');
        });
      });
    }
  });
  export let title;
</script>

<main>
  <Header title="{title}" type="{type}"/>
  <div class="{polarity}-wrapper">
    <nav class="navbar is-{polarity}" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="modernNav">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div id="modernNav" class="navbar-menu">
        <div class="navbar-start">
          <a class="navbar-item"> Home </a>
          <a class="navbar-item"> Articles </a>
          <a class="navbar-item" href="https://discord.gg/Ex3EW8P"> Chatroom </a>
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
              {#if type}<a class="button {type}" on:click={switchType}> Change Colors </a>{/if}
              {#if polarity}<a class="button" on:click={switchPolarity}>{polarity === 'dark' ? 'Day Mode' : 'Night Mode'}</a>{/if}
            </div>
          </div>
        </div>
      </div>
    </nav>
    <ArticleList fetchURL="{apiURL}" />
  </div>
</main>

<style>
  @import url('https://fonts.googleapis.com/css?family=Poiret+One&display=swap');

  .dark-wrapper {
    background: #7f00ff;
    background: -webkit-linear-gradient(to right, #7F00FF, #3f00fc) !important;
    background: linear-gradient(to right, #7F00FF, #3f00fc) !important;
    color: whitesmoke !important;
  }

  .dark-wrapper p {
    color: whitesmoke !important;
  }

  .light-wrapper {
    background: whitesmoke;
    color: black;
  }
</style>
