<script>
  import Fa from "svelte-fa";
  import { faRandom } from "@fortawesome/free-solid-svg-icons";
  import { PageTitle, LatestResults } from "../components";
  import { generateRandomNumber } from "../utils";

  let min = 1;
  let max = 10;
  let randomNumber;
  let latestRandomNumbers = [];

  const generateNumber = () => {
    if (randomNumber !== undefined)
      latestRandomNumbers = [randomNumber, ...latestRandomNumbers].filter(
        (_, index) => index <= 9
      );
    randomNumber = generateRandomNumber(min, max);
  };
</script>

<PageTitle
  ><Fa icon={faRandom} color="orangered" /> Generar número aleatorio</PageTitle
>
<div class="form">
  <div class="form-item">
    <label for="min">Mínimo:</label>
    <input
      type="number"
      bind:value={min}
      class="form-input"
      style="width: 60px;"
      name="min"
    />
  </div>
  <div class="form-item">
    <label for="max">Máximo:</label>
    <input
      type="number"
      bind:value={max}
      class="form-input"
      style="width: 60px;"
      name="max"
    />
  </div>
  <button type="button" class="btn btn-default" on:click={generateNumber}
    >¡Generar!</button
  >
</div>
<div class="number">
  {#if randomNumber === undefined}?{:else}{randomNumber}{/if}
</div>
<LatestResults results={latestRandomNumbers} />

<style>
  .form {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    margin: 25px 0px;
  }

  .number {
    text-align: center;
    font-size: 72px;
    font-weight: 700;
    background-color: #fff;
    color: orangered;
    border-radius: 4px;
    padding: 15px;
    margin-bottom: 25px;
  }
</style>
