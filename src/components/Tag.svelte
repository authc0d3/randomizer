<script>
  import { createEventDispatcher } from "svelte";
  import Fa from "svelte-fa";
  import { faTimes } from "@fortawesome/free-solid-svg-icons";

  export let id;
  export let text;
  export let closable = false;

  const dispatch = createEventDispatcher();

  const close = () => {
    dispatch("close", id);
  };
</script>

<div class="tag">
  {text}
  {#if closable}
    <span class="close" on:click={close}>
      <Fa icon={faTimes} />
    </span>
  {/if}
</div>

<style>
  .tag {
    font-size: 12px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    background-color: orangered;
    color: #fff;
    padding: 8px;
    border-radius: 4px;
  }

  .close {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 15px;
    height: 15px;
    text-align: center;
    background-color: #fff;
    color: orangered;
    border-radius: 50%;
    cursor: pointer;
    margin-left: 8px;
  }
</style>
