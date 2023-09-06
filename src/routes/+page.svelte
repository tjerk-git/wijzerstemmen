<script>
  import Statement from "$lib/components/statement.svelte";
  import Bubble from "$lib/components/bubble.svelte";
  import DragDropList, { VerticalDropZone, reorder } from "svelte-dnd-list";
  import ScoreCard from "$lib/components/scoreCard.svelte";

  const statements = [
    {
      id: 1,
      body: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    },
    {
      id: 2,
      body: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    },
  ];

  let partyAnswers = [
    {
      statement_id: 1,
      body: "Alles groen, alles links.",
      party: "Groenlinks/PVDA",
    },
    {
      statement_id: 1,
      body: "NSC all the way.",
      party: "NSC",
    },
    {
      statement_id: 1,
      body: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
      party: "VVD",
    },
    {
      statement_id: 1,
      body: "Dingen moet anders",
      party: "SP",
    },
    {
      statement_id: 1,
      body: "Wij hebben al verloren.",
      party: "CDA",
    },
  ];

  const scoreRubrix = [5, 3, 2, 0, 0];

  let scoreCard = [
    {
      party: "GroenLinks/PVDA",
      score: 0,
    },
    {
      party: "NRC",
      score: 0,
    },
    {
      party: "VVD",
      score: 0,
    },
    {
      party: "SP",
      score: 0,
    },
    {
      party: "CDA",
      score: 0,
    },
  ];

  function onDrop({ detail: { from, to } }) {
    if (!to || from === to) {
      return;
    }
    partyAnswers = reorder(partyAnswers, from.index, to.index);

    updatePartyScore();
  }

  function updatePartyScore() {
    scoreCard = partyAnswers.map((partyAnswer, index) => {
      return {
        party: partyAnswer.party,
        score: scoreRubrix[index],
      };
    });
  }
</script>

<ScoreCard {scoreCard} />

<div class="row">
  <section>
    <DragDropList
      id="party"
      type={VerticalDropZone}
      itemSize={100}
      itemCount={partyAnswers.length}
      on:drop={onDrop}
      let:index
    >
      <div class="statement" data-party-id={partyAnswers[index].party}>
        {index + 1}
        {partyAnswers[index].body}
      </div>
    </DragDropList>
  </section>
</div>

<style>
  .statement {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 2px solid black;
    padding: 2rem;
  }
  section {
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
