<script>
  import Icon from "./Icon.svelte";
  import Tag from "./Tag.svelte";

  export let icon;
  export let title;
  export let tags;
  export let closable;
  export let onRemoveTag;
</script>

<div class="tags-card">
  <h3>
    {#if icon}
      <Icon name="users" color="orangered" />{" "}
    {/if}
    {title}
  </h3>
  <div class="tags-card-body">
    {#each tags as text, i}
      <Tag id={i} bind:text bind:closable on:close={onRemoveTag} />
    {/each}
  </div>
</div>

<style>
  .tags-card {
    background-color: #fff;
    color: #434343;
    border-radius: 10px;
    padding: 15px;
  }

  .tags-card h3 {
    margin: 0 0 25px 0;
  }

  .tags-card-body {
    display: flex;
    justify-content: center;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 15px;
  }
</style>
