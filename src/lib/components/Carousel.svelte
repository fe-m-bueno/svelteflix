<script lang="ts">
  import type { MovieListResult } from "../types";
  import { media } from "../api";
  import type { View } from "../views";
  export let movies: MovieListResult[];
  export let view: View;
  export let href: string;
</script>

<h2 class="column">
  {view.title}
  {#if href}
    <a {href}>see all</a>
  {/if}
</h2>

<div class="carousel">
  {#each movies as movie}
    <a href="/movies/{movie.id}">
      <img alt={movie.title} src={media(movie.poster_path, 500)} />
    </a>
  {/each}
</div>

<style>
  .carousel {
    --padding: max(
      var(--side),
      calc(var(--side) + (100vw - var(--column)) / 2)
    );
    display: flex;
    height: clamp(10rem, 25vw, 20rem);
    overflow-x: auto;
    overflow-y: hidden;
    white-space: nowrap;
    overscroll-behavior-x: contain;
    scroll-snap-type: x mandatory;
    scroll-padding-left: var(--padding);
    padding: 0 var(--padding);
    gap: 1rem;
  }

  .carousel::-webkit-scrollbar {
    display: none;
  }

  h2 {
    font-size: 2.4rem;
    padding: 0 var(--side);
    margin-top: 4rem;
  }

  h2 a {
    color: var(--accent);
    font-size: 1.6rem;
  }

  a {
    scroll-snap-align: start;
    height: 100%;
    aspect-ratio: 2 / 3;
  }

  img {
    width: 100%;
  }
</style>
