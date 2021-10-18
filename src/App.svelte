<script>
  let start = 0
  let end = 1
  let palette = 'YlGnBu'
  let newPalette = palette
  import chroma from 'chroma-js'
  let scale = chroma.scale(palette).domain([start, end])
  let values = ''
  let inputValues = []
  // let count = [
  //   867970, 337389, 1316180, 1355122, 763410, 535943, 458201, 145778, 667080,
  // ]
  $: console.log(palette)
  $: scale = chroma.scale(palette).domain([start, end])
  $: console.log(inputValues)

  $: inputValues = inputValues
  $: convertValues(values)

  function convertValues(values) {
    let v = values.replaceAll(' ', '')

    inputValues = v.split(',')
  }

  function minMax() {
    start = Math.min(...inputValues)
    end = Math.max(...inputValues)
  }
  function updatePalette() {
    palette = newPalette
  }

  // $: console.log(values)
</script>

<main>
  <div class="inputs">
    Start: <input type="text" bind:value={start} /> &nbsp; End:
    <input type="text" bind:value={end} /><button on:click={minMax}
      >Set Min-Max
    </button>
  </div>
  <div class="inputs">
    Values: <input type="text" class="values" bind:value={values} />
  </div>
  <div class="inputs">
    Palette: <input
      type="text"
      class="palette"
      bind:value={newPalette}
    /><button on:click={updatePalette}>Change Palette</button>
  </div>
  <div class="colors">
    {#each inputValues as c}
      <div class="box-wrap">
        <div class="box" style="background: {scale(c)};" />
        <div class="label">{c}</div>
        <div class="label">{scale(c)}</div>
      </div>
    {/each}
  </div>

  <img src="./assets/images/palettes.png" alt="palettes" />
  <!-- {#each inputValues as v}
    <div>{v}</div>
  {/each} -->
</main>

<style>
  main {
    width: 600px;
    margin-left: auto;
    margin-right: auto;
    margin-top: 50px;
  }
  .values {
    width: 500px;
  }
  .inputs {
    font-size: 0.8rem;
    margin-bottom: 10px;
  }
  .colors {
    display: grid;
    grid-template-columns: repeat(9, auto);
    grid-gap: 10px;
    float: left;
  }
  .box {
    width: 50px;
    height: 50px;
    border: solid 1px lightgray;
    font-size: 0.8rem;
  }
  .label {
    font-size: 0.7rem;
    text-align: center;
  }
  button {
    margin-left: 10px;
  }
</style>
