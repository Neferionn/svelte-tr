<script>
  import PostStore from "../stores/postStore";

  export let id;
  export let userId;
  export let title;
  export let body;
  export let isAdded = false;

  const addPost = (id) => {
    let newPost = {
      id: id,
      userId: userId,
      title: title,
      body: body,
      isAdded: true,
    };

    PostStore.update((currentPosts) => {
      if (currentPosts.some((post) => post.id === id)) {
        alert("post already added");
        return [...currentPosts];
      } else {
        return [newPost, ...currentPosts];
      }
    });
  };

  const deletePost = (id) => {
    PostStore.update((posts) => {
      return posts.filter((post) => post.id !== id);
    });
  };
</script>

<div class="mt-2 flex justify-center">
  <div class="block p-6 rounded-lg shadow-lg bg-white max-w-sm">
    <h5 class="text-gray-900 text-xl leading-tight font-medium mb-2">
      {title}
    </h5>
    <p class="text-gray-700 text-base mb-4">
      {body}
    </p>

    {#if isAdded}
      <button
        type="button"
        on:click={() => {
          deletePost(id);
        }}
        class="inline-block px-6 py-2.5 bg-red-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-red-700 hover:shadow-lg focus:bg-red-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-red-800 active:shadow-lg transition duration-150 ease-in-out"
        >Delete</button
      >
    {:else}
      <button
        type="button"
        on:click={() => {
          addPost(id);
        }}
        class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out"
        >Add post</button
      >
    {/if}
  </div>
</div>
