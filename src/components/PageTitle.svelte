<script>
  import { Link } from "svelte-navigator";
  import Fa from "svelte-fa";
  import { faArrowLeft } from "@fortawesome/free-solid-svg-icons";
</script>

<h2 class="page-title">
  <Link to="/"><Fa icon={faArrowLeft} /></Link>
  <slot />
</h2>

<style>
  .page-title > :global(a) {
    display: inline-block;
    margin-right: 15px;
  }
</style>
