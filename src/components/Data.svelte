<script>
  const usersURL = "https://jsonplaceholder.typicode.com/users";

  let userInfo;

  async function getUsers() {
    const res = await fetch(usersURL);
    const users = await res.json();
    return users;
  }

  async function getUserInfo(user_ID) {
    const userURL = `${usersURL}/${user_ID}`;
    const res = await fetch(userURL);
    const data = await res.json();
    userInfo = data;
  }
</script>

<div class="flex">
  {#await getUsers() then data}
    <div class="flex flex-col items-stretch">
      {#each data as user, i}
        <div
          class="flex justify-between items-center p-2 m-1 border-2 border-blue-400 bg-slate-200"
        >
          <div class="font-bold">
            {i + 1} |
            {user.name} |
            {user.email} |
            {user.phone}
          </div>
          <button
            on:click={() => {
              getUserInfo(i + 1);
            }}
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
          >
            Details
          </button>
        </div>
      {/each}
    </div>
  {/await}
</div>

{#if !userInfo}
  <strong class="p-2"> Select user</strong>
{:else}
  <div class="flex justify-between m-2">
    <div class="p-3">
      <u>Selected user info</u> <br />
      name : <strong>{userInfo.name}</strong> <br />
      username : <strong>{userInfo.username}</strong> <br />
      email : <strong>{userInfo.email}</strong> <br />
      phone : <strong>{userInfo.phone}</strong> <br />
      website : <strong>{userInfo.website}</strong> <br />
    </div>
  </div>
{/if}
