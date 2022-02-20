<script>
  import Input from "./Input.svelte";
  let data = {
    name: "",
    email: "",
    password: "",
    emotions: [],
    satisfy: "",
  };
  let emotionTypes = ["Angry", "Sad", "Happy", "Ambivalent"];
  let satisfyOptions = [
    "Very satisfied",
    "Satisfied",
    "Didn't care",
    "Veri dissatisfied",
  ];

  const onSubmit = () => {
    console.log(data);
  };
</script>

<form
  on:submit|preventDefault={onSubmit}
  class="mt-4 p-4 border-4 border-silver-700 shadow"
>
  <legend class="text-3xl">My form</legend>
  <div class="flex flex-col">
    <Input type="text" bind:value={data.name} />
    <Input type="email" bind:value={data.email} />
    <Input type="password" bind:value={data.password} />
  </div>

  <p class="mt-2 text-xl">Please check the emotions</p>

  {#each emotionTypes as emotion}
    <label>
      <input
        type="checkbox"
        bind:group={data.emotions}
        name="emotions"
        value={emotion}
      />
      {emotion}
    </label>
  {/each}

  <p class="mt-2 text-xl">How satisfied were you with our service?</p>

  {#each satisfyOptions as satisfyOption}
    <label>
      <input
        type="radio"
        bind:group={data.satisfy}
        name="satisfy"
        value={satisfyOption}
      />
      {satisfyOption}
    </label>
  {/each}

  <button
    class="mt-3 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
    type="submit">Submit</button
  >
</form>
