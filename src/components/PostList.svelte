<script>
  import AddedPosts from "./AddedPosts.svelte";
  import SavedPostsButton from "./SavedPostsButton.svelte";
  import Card from "./Card.svelte";

  const postsURL = "https://jsonplaceholder.typicode.com/posts";

  let showPopup = false;

  let togglePopup = () => {
    showPopup = !showPopup;
  };

  const getPosts = async () => {
    const res = await fetch(postsURL);
    const posts = await res.json();
    return posts.slice(0, 30);
  };
</script>

<AddedPosts {showPopup} on:click={togglePopup} />
<main class="container mx-auto px-4">
  <SavedPostsButton on:click={togglePopup} />
  <div class="flex justify-center">
    {#await getPosts() then data}
      <div class="grid grid-cols-3 gap-3">
        {#each data as post, i}
          <Card {...post} />
        {/each}
      </div>
    {/await}
  </div>
</main>
