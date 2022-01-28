<script>
  import Fa from "svelte-fa";
  import {
    faTrophy,
    faPlus,
    faRandom,
    faRedo
  } from "@fortawesome/free-solid-svg-icons";
  import { PageTitle, TagsCard } from "../components";
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

<PageTitle><Fa icon={faTrophy} color="orangered" /> Realizar sorteo</PageTitle>
{#if !winner}
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
        >Escriba un participante por línea para agregar varios a la vez</span
      >
    </div>
    <button type="submit" class="btn btn-default">
      <Fa icon={faPlus} color="orangered" />{" "}
      Añadir
    </button>
  </form>
{/if}
{#if competitorList.length > 0}
  <TagsCard
    title="Participantes"
    tags={competitorList}
    onRemoveTag={handleRemoveCompetitor}
    closable={!winner}
  />
  {#if competitorList.length > 1 && !winner}
    <div class="raffle-button">
      <button class="btn btn-default" type="button" on:click={handleRaffle}
        ><Fa icon={faRandom} color="orangered" /> ¡Elegir un ganador!</button
      >
    </div>
  {/if}
  {#if winner}
    <div class="winner">
      <h3>Y el ganador es...</h3>
      <h1><Fa icon={faTrophy} color="orangered" /> {winner}</h1>
      <div class="congrats" />
    </div>
    <div class="redo">
      <button
        class="btn btn-default"
        type="button"
        on:click={() => (winner = undefined)}
      >
        <Fa icon={faRedo} color="orangered" /> Volver a sortear
      </button>
    </div>
  {/if}
{/if}

<style>
  .form {
    margin: 35px 0 25px 0;
  }

  .raffle-button {
    text-align: center;
    margin: 15px 0 25px 0;
  }

  .winner {
    background-color: #fff;
    color: #434343;
    border-radius: 10px;
    text-align: center;
    padding: 15px;
    font-size: 16px;
    margin: 25px 0;
  }

  .winner h3 {
    font-size: 16px;
    font-weight: 400;
    margin-bottom: 15px;
  }

  .winner h1 {
    margin-bottom: 20px;
  }

  .congrats {
    background-image: url("../img/congrats.gif");
    background-position: center center;
    background-repeat: no-repeat;
    background-size: cover;
    margin: 0 auto;
    height: 160px;
    width: 90%;
    max-width: 400px;
    border-radius: 10px;
  }

  .redo {
    text-align: center;
  }
</style>
