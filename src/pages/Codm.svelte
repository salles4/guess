<script>
  import wrongSfx from "../assets/wrong.mp3";
  import correctSfx from "../assets/correct.mp3";
  import completeSfx from "../assets/complete.mp3";
  import { slide } from "svelte/transition";

  const MAPS = [
    "Bus Station",
    "Circus",
    "Countdown",
    "Crash",
    "Diner",
    "Dock",
    "Estate",
    "Farm",
    "Forest",
    "Killhouse",
    "Launch Base",
    "Nuclear Plant",
    "Nuketown",
    "Overgrown",
    "Pier",
    "Pipeline",
    "Practice Range",
    "Sakura",
    "Standoff",
    "Isolated"
  ]
let mapPool = MAPS;

let selectedMap = "Welcome!";
let mapUrl = "2";
let choices = []
let score = 0

function randomize(){
  const randomIndex = Math.floor(Math.random() * mapPool.length)
  
  selectedMap = mapPool[randomIndex] 
  mapUrl = selectedMap != "Isolated" ? selectedMap.split(" ").join("").toLowerCase() : "overview";
  
  mapPool.splice(randomIndex, 1)
  mapPool = [...mapPool]
  
  choices = []
  choices.push(selectedMap)
  while(choices.length < 4){
    const randomMapIndex = Math.floor(Math.random() * MAPS.length)
    if(!choices.includes(MAPS[randomMapIndex])){
      choices.push(MAPS[randomMapIndex])
    }
  }
  choices.sort(() => Math.random() - 0.5)
  choices = [...choices]
}

function answer(e){
  if(e.target.innerHTML == selectedMap){
    score += 1
    new Audio(correctSfx).play();
  }else{
    new Audio(wrongSfx).play();
  }
  if(mapPool.length > 0){
    randomize()
  }else{
    choices = []
    let completeAudio = new Audio(completeSfx);
        completeAudio.volume = 0.9;
        completeAudio.play();
  }
}

</script>

<main class="p-4" in:slide>
  <div>
    <a href="./#/" class="btn btn-error">Back</a>
    <button class="btn btn-primary" on:click={randomize}>Start</button> 
  </div>
  <div class="text-2xl inline text-white">Score: {score} | Maps Left: {mapPool.length}</div>
  <img class="w-[100vh] object-contain mb-2" src="https://callofdutymaps.com/wp-content/uploads/isolated{mapUrl}.jpg" alt="br map">
  <div class="grid grid-cols-2 gap-2">
    {#each choices as choice}
    <button class="btn btn-primary text-xl text-white" on:click={answer}>{choice}</button>
    {/each}
  </div>
</main>