<script>
  import { PageTitle, Tag } from "../components";
  import { generateRandomNumber } from "../utils";

  let competitor = "";
  let competitorList = [];
  let winner;

  const addCompetitor = event => {
    event.preventDefault();
    if (competitor.trim() === "") return;
    competitorList = [
      ...competitorList,
      ...competitor.split("\n").filter(name => name.trim() !== "")
    ];
    competitor = "";
  };

  const handleRemoveCompetitor = ({ detail: index }) => {
    competitorList = [...competitorList.filter((_, i) => i !== index)];
  };

  const handleRaffle = () => {
    const winnerIndex = generateRandomNumber(0, competitorList.length - 1);
    winner = competitorList[winnerIndex];
  };
</script>

<PageTitle>🏆 Realizar sorteo</PageTitle>
<form class="form" on:submit={addCompetitor}>
  <div class="form-item form-item-horizontal">
    <label for="competitor">Añadir participantes:</label>
    <textarea
      type="text"
      bind:value={competitor}
      class="form-input"
      name="competitor"
      rows="5"
    />
    <span class="form-item-info"
      >Escriba un participante por linea para agregar varios a la vez</span
    >
  </div>
  <button type="submit" class="btn btn-default">Añadir</button>
</form>
{#if competitorList.length > 0}
  <div class="competitors">
    <h3>👪 Participantes</h3>
    <div class="competitor-list">
      {#each competitorList as name, i}
        <Tag id={i} text={name} on:close={handleRemoveCompetitor} closable />
      {/each}
    </div>
  </div>
  {#if competitorList.length > 1}
    <div class="raffle-button">
      <button class="btn btn-default" type="button" on:click={handleRaffle}
        >¡Elegir un ganador!</button
      >
    </div>
  {/if}
  {#if winner}
    <div class="winner">
      <h3>Y el ganador es...</h3>
      <h1>🏆 {winner}</h1>
    </div>
  {/if}
{/if}

<style>
  .form {
    margin-bottom: 25px;
  }

  .competitors {
    border: 2px solid #fff;
    border-radius: 10px;
    padding: 15px;
  }

  .competitors h3 {
    margin: 0 0 25px 0;
  }

  .competitor-list {
    display: flex;
    justify-content: center;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 15px;
  }

  .raffle-button {
    text-align: center;
    margin: 15px 0 25px 0;
  }

  .winner {
    border: 2px solid #fff;
    border-radius: 10px;
    text-align: center;
    padding: 15px;
  }

  .winner h3 {
    font-weight: 300;
    margin-bottom: 15px;
  }
</style>
