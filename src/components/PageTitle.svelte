<script>
  import { Link } from "svelte-navigator";
  import Icon from "./Icon.svelte";
</script>

<h2 class="page-title">
  <Link to="/"><Icon name="arrow-left" /></Link>
  <slot />
</h2>

<style>
  .page-title > :global(a) {
    display: inline-block;
    margin-right: 15px;
  }
</style>
