<script lang="ts">
  import { media } from "$lib/api";
  import type { MovieDetails } from "$lib/types";
  import type { Image } from "../../../lib/types";

  export let movie: MovieDetails;

  $: backdrop =
    movie.images.backdrops.find((image) => !image.iso_639_1) ||
    movie.images.backdrops[0];
</script>

<div class="featured">
  <div class="backdrop">
    <img
      alt={movie.title}
      src={media(backdrop.file_path, 1280)}
      style="aspect-ratio: {backdrop.aspect_ratio}"
    />
  </div>

  <div class="info">
    <h1>{movie.title}</h1>
    <p>{movie.overview}</p>
  </div>
</div>

<style>
  .featured {
    position: relative;
    display: grid;
    background: black;
  }

  .backdrop img {
    width: 100%;
    display: block;
  }

  .backdrop::after {
    content: "";
    position: absolute;
    width: 100%;
    height: 8rem;
    left: 0;
    bottom: 0;
    background: linear-gradient(to top, black, transparent);
  }

  .info {
    display: flex;
    flex-direction: column;
    bottom: 0;
    width: 100%;
    padding: var(--side);
    margin-top: -4rem;
    gap: 1rem;
  }

  .info h1,
  .info p {
    margin: 0;
  }

  .info p {
    max-width: 40ch;
  }

  @media (min-width: 80em) {
    .featured {
      grid-template-columns: 1fr 80em;
      grid-template-rows: auto;
    }

    .info {
      position: absolute;
      justify-content: center;
      top: 0;
      left: 0;
      width: 40em;
      height: 100%;
      grid-column: 1/2;
      margin: 0;
    }

    .backdrop {
      grid-column: 2/3;
    }

    .backdrop::after {
      width: 15rem;
      height: 100%;
      left: 100px;
      left: 0;
      bottom: 0;
      background: linear-gradient(to right, black, transparent);
    }
  }
</style>
