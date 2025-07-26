<script lang="ts">
  const index0: [number, number] = $state([0, 0]);
  const index1: [number, number] = $state([1, 1]);

  function randomBool() {
    return Math.random() < 0.5;
  }
  function onclick() {
    const indexToChange = randomBool() ? [index0, index1] : [[index0, index1][+randomBool()]];
    for (const index of indexToChange) {
      const i = +randomBool(),
        j = +!i;
      index[i] = +!index[i];
      if (randomBool()) {
        index[j] = +!index[j];
      }
    }
  }

  function createDendekodon(index: [number, number], charset: string[] | string[][]) {
    return charset.map((v, i) => v[index[i]]).join("");
  }
  const kiageDendekodonJp = $derived(
    `きあげ・${[index0, index1].map(index => createDendekodon(index, ["でど", "こん"])).join("")}どん`,
  );
  const kiageDendekodonEn = $derived(
    `KIAGE ${[index0, index1]
      .map(index =>
        createDendekodon(index, [
          ["DE", "DO"],
          ["KO", "N"],
        ]),
      )
      .join("")}DON`,
  );
</script>

<main class="grid h-dvh place-content-center bg-radial from-blue-400 to-blue-200 text-white">
  <div class="w-[80dvw] text-center break-words">
    <button class="cursor-pointer text-7xl" {onclick}>{kiageDendekodonJp}</button>
    <hr class="my-10 border" />
    <p class="text-5xl">{kiageDendekodonEn}</p>
  </div>
</main>
