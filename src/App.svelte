<script>
  import Header from './components/Header.svelte';
  import ArticleList from './components/articles/ArticleList.svelte';

  const apiURL = 'https://the-modern-farm.herokuapp.com/article/all';
  let polarity = 'light', polarityBtn = 'Night Mode', nextPolarity = 'grey';
  let data = [], type = 'is-dark';

  const switchPolarity = () => {
    switch(polarity){
      case 'light':
        polarity = nextPolarity;
        nextPolarity = 'dark';
        polarityBtn = '90\'s Mode';
        break;
      case 'grey':
        polarity = nextPolarity;
        nextPolarity = 'light';
        polarityBtn = 'Day Mode';
        break;
      default:
        polarity = nextPolarity;
        nextPolarity = 'grey';
        polarityBtn = 'Night Mode';
    }
  };
  const switchToPrimary = async() => {type = ''; setTimeout(() => {type = 'is-primary'}, 1000); };
  const switchToSuccess = async() => {type = ''; setTimeout(() => {type = 'is-success'}, 1000); };
  const switchToDanger = async() => {type = ''; setTimeout(() => {type = 'is-danger'}, 1000); };
  const switchToWarning = async() => {type = ''; setTimeout(() => {type = 'is-warning'}, 1000); };
  const switchToInfo = async() => {type = ''; setTimeout(() => {type = 'is-info'}, 1000); };
  const switchToLink = async() => {type = ''; setTimeout(() => {type = 'is-link'}, 1000); };
  const switchToDark = async() => {type = ''; setTimeout(() => {type = 'is-dark'}, 1000); };

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
    <nav class="navbar is-{polarity === 'light' ? 'light' : 'dark'}" role="navigation" aria-label="main navigation">
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
              {#if type}
                <a class="button is-primary" on:click={switchToPrimary}>&nbsp;</a>
                <a class="button is-success" on:click={switchToSuccess}>&nbsp;</a>
                <a class="button is-danger" on:click={switchToDanger}>&nbsp;</a>
                <a class="button is-warning" on:click={switchToWarning}>&nbsp;</a>
                <a class="button is-info" on:click={switchToInfo}>&nbsp;</a>
                <a class="button is-link" on:click={switchToLink}>&nbsp;</a>
                <a class="button is-dark" on:click={switchToDark}>&nbsp;</a>
              {/if}
              {#if polarity}<a class="button {nextPolarity}-wrapper" on:click={switchPolarity}>{polarityBtn}</a>{/if}
            </div>
          </div>
        </div>
      </div>
    </nav>
    <ArticleList fetchURL="{apiURL}" polarity="{polarity}" />
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

  .grey-wrapper {
    background: #333333;
    background: -webkit-linear-gradient(to right, #333333, #222222) !important;
    background: linear-gradient(to right, #333333, #222222) !important;
    color: whitesmoke;
  }

  .light-wrapper {
    background: whitesmoke;
    color: black;
  }
</style>
