<script>
  import PostStore from "../stores/postStore";
  import Card from "./Card.svelte";

  export let showPopup = false;
</script>

{#if showPopup}
  <div class="w-full h-full fixed back-shadow" on:click|self>
    <div class="w-9/12 mt-6 mb-6 h-full overflow-auto mx-auto bg-white rounded">
      <p
        class="m-2 p-2 text-3xl text-center uppercase border-4 border-white border-b-indigo-500"
      >
        Added posts list
      </p>
      <div class="grid grid-cols-3 gap-1">
        {#each $PostStore as post, i}
          <Card {...post} />
        {:else}
          <div
            class="w-9/12 fixed h-full flex justify-center items-center content-center"
          >
            <p class="text-6xl">This list is empty</p>
          </div>
        {/each}
      </div>
    </div>
  </div>
{/if}

<style>
  .back-shadow {
    background: rgba(0, 0, 0, 0.8);
  }
</style>
