<script>
  import { page } from "$app/stores";
  import "../styles.css";
  import logo from "$lib/images/logo.svg";
  import TMDB from "$lib/images/tmdb.svg";
</script>

<nav>
  <a class="logo" href="/">
    <img class="logo" src={logo} alt="Svelteflix" />
  </a>
  <div class="links">
    <a href="/search">Search</a>
    <a href="/watchlist">Watchlist</a>
    <a href="/login">Log in</a>
  </div>
</nav>

<main class:infinite={$page.data.infinite}>
  <slot />
</main>

<footer>
  <p>
    Data provided by
    <a href="https://www.themoviedb.org/">
      <img src={TMDB} alt="The Movie DB" />
    </a>
  </p>
</footer>

<style>
  nav,
  footer {
    padding: 1rem var(--side);
    margin: 0 auto;
  }

  nav {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: space-between;
    color: var(--accent);
    max-width: var(--column);
  }

  footer {
    display: flex;
    height: 5rem;
    align-items: center;
  }

  a {
    text-decoration: none;
  }

  .links {
    display: flex;
    align-items: center;
  }

  main.infinite {
    height: 0;
    flex: 1;
    overflow: hidden;
  }

  .links {
    display: flex;
    gap: 1em;
  }

  .logo {
    display: block;
    overflow: auto;
    height: 100%;
  }
</style>
