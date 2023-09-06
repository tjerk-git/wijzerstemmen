<script>
  export let scoreCard;
</script>

<div class="score-card">
  {#each scoreCard as party (party.party)}
    <div class="party">
      <p>{party.party}</p>
      {party.score}
    </div>
  {/each}
</div>

<style>
  .party {
    border-radius: 100%;
    background-color: red;
    color: white;
    width: 10rem;
    height: 10rem;
    text-align: center;
    transition: all 0.5s;
    font-size: 3rem;
  }
  .score-card {
    position: fixed;
    display: flex;
    flex-direction: column;
    right: 5%;
    top: 10%;
    transition: all 0.5s;
  }
</style>
