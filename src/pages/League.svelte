<script>
  import wrongSfx from "../assets/wrong.mp3";
  import correctSfx from "../assets/correct.mp3";
  import completeSfx from "../assets/complete.mp3";
  import { slide } from "svelte/transition";
  let champJson;
  let CHAMPLIST;

  let selectedChamp = "";
  let selectedChampKey;

  let choices = [];
  let score = 0;
  async function getChampData() {
    const response = await fetch(
      "https://ddragon.leagueoflegends.com/cdn/14.14.1/data/en_US/champion.json"
    );
    const data = await response.json();
    champJson = data.data;
    CHAMPLIST = Object.keys(champJson);
    console.log(CHAMPLIST);
  }
  getChampData();

  function randomize() {
    selectedChampKey = "";
    setTimeout(()=>{},100)
    const selectedIndex = Math.floor(Math.random() * CHAMPLIST.length);
    const champObj = champJson[CHAMPLIST[selectedIndex]];
    selectedChamp = champObj.name;
    selectedChampKey = ""
    selectedChampKey = champObj.key;
    // new Audio(`https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-choose-vo/${selectedChampKey}.ogg`).play()

    choices = [];
    choices.push(CHAMPLIST[selectedIndex]);
    
    while (choices.length < 4) {
      const choiceIndex = Math.floor(Math.random() * CHAMPLIST.length);
      if (!choices.includes(CHAMPLIST[choiceIndex])) {
        choices.push(CHAMPLIST[choiceIndex]);
      }
    }
    choices.sort(() => Math.random() - 0.5);
    choices = [...choices];
  }

  function answer(e) {
    if (e.target.getAttribute("data-name") == selectedChamp) {
      score += 1;
      new Audio(correctSfx).play();
    } else {
      new Audio(wrongSfx).play();
      score -= 1;
    }
    if (score != 10) {
      randomize();
    } else {
      choices = [];
      let completeAudio = new Audio(completeSfx);
      completeAudio.volume = 0.9;
      completeAudio.play();
      selectedChampKey = ""
      score = 0
    }
  }
  const skills = ["q", "w", "e", "r", "passive"]
  function getSkill(){
    return skills[Math.floor(Math.random() * skills.length)]
  }
</script>

<main in:slide>
  <div
    class="flex flex-col items-center justify-evenly gap-3 backdrop-blur-md bg-transparent text-white border-2 border-gray-900 rounded p-4"
  >
  
    {#if selectedChampKey }
      <div>Score: {score}/10</div>
      <img class="h-[128px]" src="https://cdn.communitydragon.org/latest/champion/{selectedChampKey}/ability-icon/{getSkill()}" alt="">
      <div class="grid grid-cols-2 gap-2">
        {#each choices as champKey}
        <button data-name={champJson[champKey].name} class="btn btn-primary text-white h-auto grid grid-cols-2" on:click={answer}
        ><img data-name={champJson[champKey].name} class="h-[64px]" src="https://raw.communitydragon.org/latest/plugins/rcp-be-lol-game-data/global/default/v1/champion-icons/{champJson[champKey].key}.png" alt="">{champJson[champKey].name}</button
        >
        {/each}
      </div>
    {:else}
    <img
    class="w-[256px]"
    src="https://cmsassets.rgpub.io/sanity/images/dsfx7636/news/9eb028de391e65072d06e77f06d0955f66b9fa2c-736x316.png?auto=format&fit=fill&q=80&w=625"
    alt="league logo"
    />
    <div>
    <a href="./#/" class="btn btn-error btn-sm text-white">Back</a>
    <button class="btn btn-primary btn-sm text-white" on:click={randomize}>Start</button>
  </div>
    {/if}
  </div>
</main>
