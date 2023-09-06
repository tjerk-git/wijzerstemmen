<script>
  export let party;

  let count = 0;

  $count: {
    if (count > 0) {
      console.log("i have changed");
    }
  }
</script>

<div class="party">
  <p>{party}</p>
</div>

<style>
  .party {
    border-radius: 100%;
    width: 5rem;
    height: 5rem;
  }
</style>
