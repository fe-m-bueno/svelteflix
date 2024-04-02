<script lang="ts">
  import { media } from "../lib/api";
  import type { MovieDetails } from "../lib/types";

  export let movie: MovieDetails;

  $: images = movie.images;
  $: backdrop =
    images.backdrops.find((image) => !image.iso_639_1) || images.backdrops[0];
  $: logo =
    images.logos.find((image) => image.iso_639_1 === "en") ||
    images.backdrops[0];
</script>

<a href="/movies/{movie.id}" class="column">
  <img
    class="backdrop"
    alt={movie.title}
    src={media(backdrop.file_path, 1280)}
    style="aspect-ratio: {backdrop.aspect_ratio}"
  />

  <img
    class="logo"
    alt={movie.title}
    src={media(logo.file_path, 500)}
    style="aspect-ratio: {logo.aspect_ratio}"
  />
</a>

<style>
  a {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .backdrop {
    width: 100%;
  }

  .logo {
    position: absolute;
    width: 20%;
    height: 50%;
    left: 20em;
    top: 13em;
    object-fit: contain;
    object-position: 50% 75%;
    filter: drop-shadow(0 0 3rem black) drop-shadow(0 0 0.5rem black);
  }
</style>
