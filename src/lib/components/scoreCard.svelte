<script>
  export let scoreCard;
</script>

<div class="party">
  {#each scoreCard as party}
    <p>{party.party}</p>
    <p>{party.score}</p>
  {/each}
</div>
