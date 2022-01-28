<script>
  import { PageTitle, TagsCard, Icon } from "../components";
  import { generateRandomNumber } from "../utils";

  let item = "";
  let itemList = [];
  let numGroups = 2;
  let groups = [];

  const addItem = event => {
    event.preventDefault();
    if (item.trim() === "") return;
    itemList = [
      ...itemList,
      ...item.split("\n").filter(name => name.trim() !== "")
    ];
    item = "";
  };

  const handleRemoveItem = ({ detail: index }) => {
    itemList = [...itemList.filter((_, i) => i !== index)];
  };

  const getSmallerGroupIndex = _groups => {
    return _groups.reduce((smaller, group, index) => {
      if (group.length < _groups[smaller].length) smaller = index;
      return smaller;
    }, 0);
  };

  const handleCreateGroups = () => {
    const _groups = [...Array(numGroups).keys()].map(() => []);
    let _itemList = [...itemList];
    itemList.forEach(() => {
      const randomItemIndex = generateRandomNumber(0, _itemList.length - 1);
      const randomItem = _itemList[randomItemIndex];
      _itemList.splice(randomItemIndex, 1);
      const smallerGroupIndex = getSmallerGroupIndex(_groups);
      _groups[smallerGroupIndex].push(randomItem);
    });
    groups = _groups;
  };
</script>

<PageTitle
  ><Icon name="users" color="orangered" /> Generar grupos aleatorios</PageTitle
>
{#if !groups.length}
  <form class="form" on:submit={addItem}>
    <div class="form-item">
      <label for="numGroups">Nº de Grupos:</label>
      <input
        type="number"
        min="2"
        class="form-input"
        name="numGroups"
        bind:value={numGroups}
        style="width: 60px;"
      />
    </div>
    <div class="form-item form-item-horizontal">
      <label for="competitor">Añadir integrantes:</label>
      <textarea
        type="text"
        bind:value={item}
        class="form-input"
        name="competitor"
        rows="5"
      />
      <span class="form-item-info"
        >Escriba un integrante por línea para agregar varios a la vez</span
      >
    </div>
    <button type="submit" class="btn btn-default">
      <Icon name="plus" color="orangered" />{" "}
      Añadir
    </button>
  </form>
{/if}
{#if itemList.length > 0}
  <TagsCard
    title="Integrantes"
    icon="users"
    tags={itemList}
    onRemoveTag={handleRemoveItem}
    closable={!groups.length}
  />
  {#if itemList.length >= numGroups && !groups.length}
    <div class="create-groups">
      <button
        class="btn btn-default"
        type="button"
        on:click={handleCreateGroups}
        ><Icon name="random" color="orangered" /> ¡Crear grupos al azar!</button
      >
    </div>
  {/if}
  {#if groups.length > 0}
    <div class="group-list">
      {#each groups as group, i}
        <div class="group">
          <h4>Grupo {i + 1}</h4>
          <div class="group-content">
            <ul>
              {#each group as item}
                <li>{item}</li>
              {/each}
            </ul>
          </div>
        </div>
      {/each}
    </div>
    <div class="redo">
      <button
        class="btn btn-default"
        type="button"
        on:click={() => (groups = [])}
      >
        <Icon name="redo" color="orangered" /> Volver a sortear
      </button>
    </div>
  {/if}
{/if}

<style>
  .form {
    margin: 35px 0 25px 0;
  }

  .form .form-item {
    margin-bottom: 15px;
  }

  .create-groups {
    text-align: center;
    margin: 15px 0 25px 0;
  }

  .group-list {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: flex-start;
    gap: 3%;
    row-gap: 15px;
    margin: 25px 0;
  }

  .group {
    width: 31%;
    background-color: #fff;
    color: #535353;
    border-radius: 5px;
    line-height: 1.4em;
    overflow: hidden;
  }

  .group h4 {
    color: #fff;
    background-color: orangered;
    margin: 0;
    padding: 8px 12px;
  }

  .group .group-content {
    padding: 12px;
  }

  .group .group-content ul {
    margin: 0 20px;
  }

  .redo {
    text-align: center;
  }

  @media (max-width: 768px) {
    .group {
      width: 48%;
    }
  }

  @media (max-width: 521px) {
    .group-list {
      flex-direction: column;
      gap: 15px;
    }
    .group {
      width: 100%;
    }
  }
</style>
