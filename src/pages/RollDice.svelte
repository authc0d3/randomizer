<script>
  import { onMount } from "svelte";
  import { generateRandomNumber } from "../utils";
  import { PageTitle, LatestResults, Icon } from "../components";

  let side = 1;
  let firstRoll = true;
  let latestRolls = [];

  const rollDice = () => {
    if (!firstRoll) {
      latestRolls = [side, ...latestRolls].filter((_, index) => index <= 9);
    }
    side = generateRandomNumber(1, 6);
    const dice = document.querySelector(".face-list");
    dice.classList.toggle("odd-roll");
    dice.classList.toggle("even-roll");
    firstRoll = false;
  };

  // NOTE: We need to remove odd-roll class to make dice work fine.
  // We add this class to force svelt to add these styles.
  onMount(() => {
    const dice = document.querySelector(".face-list");
    dice.classList.toggle("odd-roll");
  });
</script>

<PageTitle><Icon name="dice" color="orangered" /> Tirar un dado</PageTitle>
<p class="dice-info">¡Haz click sobre el dado para lanzarlo!</p>
<div class="dice" on:click={rollDice}>
  <ol class="face-list even-roll odd-roll" data-roll={side}>
    <li class="face" data-side="1">
      <span class="dot" />
    </li>
    <li class="face" data-side="2">
      <span class="dot" />
      <span class="dot" />
    </li>
    <li class="face" data-side="3">
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
    </li>
    <li class="face" data-side="4">
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
    </li>
    <li class="face" data-side="5">
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
    </li>
    <li class="face" data-side="6">
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
      <span class="dot" />
    </li>
  </ol>
</div>
<br />
<LatestResults results={latestRolls} />

<style>
  .dice-info {
    text-align: center;
    margin-bottom: 25px;
  }

  .dice {
    align-items: center;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(8rem, 1fr));
    grid-template-rows: auto;
    justify-items: center;
    padding: 80px 0;
    perspective: 600px;
    cursor: pointer;
  }

  .face-list {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr;
    height: 6rem;
    list-style-type: none;
    transform-style: preserve-3d;
    width: 6rem;
  }
  .even-roll {
    transition: transform 1.5s ease-out;
  }
  .odd-roll {
    transition: transform 1.25s ease-out;
  }
  .face {
    background-color: #fefefe;
    box-shadow: inset -0.35rem 0.35rem 0.75rem rgba(0, 0, 0, 0.3),
      inset 0.5rem -0.25rem 0.5rem rgba(0, 0, 0, 0.15);
    display: grid;
    grid-column: 1;
    grid-row: 1;
    grid-template-areas:
      "one two three"
      "four five six"
      "seven eight nine";
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    height: 100%;
    padding: 1rem;
    width: 100%;
  }
  .dot {
    align-self: center;
    background-color: orangered;
    border-radius: 50%;
    box-shadow: inset -0.15rem 0.15rem 0.25rem rgba(0, 0, 0, 0.5);
    display: block;
    height: 1.25rem;
    justify-self: center;
    width: 1.25rem;
  }
  .even-roll[data-roll="1"] {
    transform: rotateX(360deg) rotateY(720deg) rotateZ(360deg);
  }
  .even-roll[data-roll="2"] {
    transform: rotateX(450deg) rotateY(720deg) rotateZ(360deg);
  }
  .even-roll[data-roll="3"] {
    transform: rotateX(360deg) rotateY(630deg) rotateZ(360deg);
  }
  .even-roll[data-roll="4"] {
    transform: rotateX(360deg) rotateY(810deg) rotateZ(360deg);
  }
  .even-roll[data-roll="5"] {
    transform: rotateX(270deg) rotateY(720deg) rotateZ(360deg);
  }
  .even-roll[data-roll="6"] {
    transform: rotateX(360deg) rotateY(900deg) rotateZ(360deg);
  }
  .odd-roll[data-roll="1"] {
    transform: rotateX(-360deg) rotateY(-720deg) rotateZ(-360deg);
  }
  .odd-roll[data-roll="2"] {
    transform: rotateX(-270deg) rotateY(-720deg) rotateZ(-360deg);
  }
  .odd-roll[data-roll="3"] {
    transform: rotateX(-360deg) rotateY(-810deg) rotateZ(-360deg);
  }
  .odd-roll[data-roll="4"] {
    transform: rotateX(-360deg) rotateY(-630deg) rotateZ(-360deg);
  }
  .odd-roll[data-roll="5"] {
    transform: rotateX(-450deg) rotateY(-720deg) rotateZ(-360deg);
  }
  .odd-roll[data-roll="6"] {
    transform: rotateX(-360deg) rotateY(-900deg) rotateZ(-360deg);
  }
  [data-side="1"] {
    transform: rotate3d(0, 0, 0, 90deg) translateZ(4rem);
  }
  [data-side="2"] {
    transform: rotate3d(-1, 0, 0, 90deg) translateZ(4rem);
  }
  [data-side="3"] {
    transform: rotate3d(0, 1, 0, 90deg) translateZ(4rem);
  }
  [data-side="4"] {
    transform: rotate3d(0, -1, 0, 90deg) translateZ(4rem);
  }
  [data-side="5"] {
    transform: rotate3d(1, 0, 0, 90deg) translateZ(4rem);
  }
  [data-side="6"] {
    transform: rotate3d(1, 0, 0, 180deg) translateZ(4rem);
  }
  [data-side="1"] .dot:nth-of-type(1) {
    grid-area: five;
  }
  [data-side="2"] .dot:nth-of-type(1) {
    grid-area: one;
  }
  [data-side="2"] .dot:nth-of-type(2) {
    grid-area: nine;
  }
  [data-side="3"] .dot:nth-of-type(1) {
    grid-area: one;
  }
  [data-side="3"] .dot:nth-of-type(2) {
    grid-area: five;
  }
  [data-side="3"] .dot:nth-of-type(3) {
    grid-area: nine;
  }
  [data-side="4"] .dot:nth-of-type(1) {
    grid-area: one;
  }
  [data-side="4"] .dot:nth-of-type(2) {
    grid-area: three;
  }
  [data-side="4"] .dot:nth-of-type(3) {
    grid-area: seven;
  }
  [data-side="4"] .dot:nth-of-type(4) {
    grid-area: nine;
  }
  [data-side="5"] .dot:nth-of-type(1) {
    grid-area: one;
  }
  [data-side="5"] .dot:nth-of-type(2) {
    grid-area: three;
  }
  [data-side="5"] .dot:nth-of-type(3) {
    grid-area: five;
  }
  [data-side="5"] .dot:nth-of-type(4) {
    grid-area: seven;
  }
  [data-side="5"] .dot:nth-of-type(5) {
    grid-area: nine;
  }
  [data-side="6"] .dot:nth-of-type(1) {
    grid-area: one;
  }
  [data-side="6"] .dot:nth-of-type(2) {
    grid-area: three;
  }
  [data-side="6"] .dot:nth-of-type(3) {
    grid-area: four;
  }
  [data-side="6"] .dot:nth-of-type(4) {
    grid-area: six;
  }
  [data-side="6"] .dot:nth-of-type(5) {
    grid-area: seven;
  }
  [data-side="6"] .dot:nth-of-type(6) {
    grid-area: nine;
  }
</style>
