<script>
  export let type, value;

  const typeAction = (node) => {
    node.type = type;
  };
</script>

<input class="mt-2" use:typeAction bind:value required />
