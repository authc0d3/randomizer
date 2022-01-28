<script>
  import Fa from "svelte-fa";
  import {
    faCommentDots,
    faArrowLeft,
    faDice,
    faHome,
    faPlus,
    faRandom,
    faRedo,
    faTimes,
    faTrophy,
    faUsers
  } from "@fortawesome/free-solid-svg-icons";

  const icons = {
    "comment-dots": faCommentDots,
    "arrow-left": faArrowLeft,
    dice: faDice,
    home: faHome,
    plus: faPlus,
    random: faRandom,
    redo: faRedo,
    times: faTimes,
    trophy: faTrophy,
    users: faUsers
  };

  export let color;
  export let size;
  export let name;
</script>

<Fa icon={icons[name]} {color} {size} />
