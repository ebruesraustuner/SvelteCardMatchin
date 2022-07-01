<script>
  import Sailor from "./Sailor.svelte";

  let play = false;
  let selected;
  let selectedCards = []
  $: console.log('selected cardID', selected);

  let isBack = false;
  let list = [
    {
      name: "teset",
      surname: "testsur",
      id: "1",
    },
    {
      name: "teset",
      surname: "testsur",
      id: "1",
    },
    {
      name: "teset2",
      surname: "testsur2",
      id: "2",
    },
    {
      name: "teset3",
      surname: "testsur3",
      id: "3",
    },
    {
      name: "teset4",
      surname: "testsur4",
      id: "4",
    },
  ];

  let canFlipped = false

  const toggleBackFront = (e) => {
    
    console.log("🚀 ~ file: App.svelte ~ line 46 ~ toggleBackFront ~ e", e)
    
     selected = Number(e.i);
    list.forEach((item) =>{ 
        return {
          ...item,
          flipped: false
        }
    });
    // let selectedCard = list.filter((i) => i.i === e.id)
   
    // console.log("🚀 ~ file: App.svelte ~ line 53 ~ toggleBackFront ~ selectedCard[0].id", selectedCard[0].id)
    // canFlipped = selectedCard[0].id === e.id
    // selectedCards = [...selectedCards, ...selectedCard]
    // console.log("🚀 ~ file: App.svelte ~ line 48 ~ toggleBackFront ~ selectedCards", selectedCards)
  };
  
</script>

<main class="main">
  {#if !play}
    <div class="welcome">
      <h1 style="position: absolute; top: 56px;">Welcome</h1>
      <button on:click={() => (play = !play)} class="btn"
        ><div class="ply" /></button
      >
    </div>
  {:else}
    <div class="grid-list">
      {#each list as { name, surname, id, flipped}, i}
        <div class="grid-container">
          <button  data-card-id={i} id={id}
            >Çevir {isBack}</button
          >
          <div class="card-list" on:click={() => toggleBackFront({i})} data-card-id={i} id={id}>
           seöilen {selected} id {id} flipped {canFlipped}
            <div class="card" class:show-back={selected === i} >
              <div class="card-front">front</div>
              <div class="card-back">
                back
                {name} , {surname}
              </div>
            </div>
          </div>
        </div>
      {/each}
    </div>
  {/if}
</main>

<style>
  .main {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
  }
  .btn {
    background-image: url("./img/art.png");
    width: 204px;
    height: 75px;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
    background-color: transparent;
    border: none;
    position: relative;
  }

  .btn:hover {
    margin-top: 4px;
  }

  .btn:after {
    content: "";
    width: 120px;
    height: 4px;
    background-color: white;
    position: absolute;
    top: 10px;
    left: 30px;
    opacity: 0.5;
  }
  .btn:before {
    content: "";
    width: 160px;
    height: 8px;
    position: absolute;
    bottom: 8px;
    right: 22px;
    opacity: 0.5;
    background: rgb(235, 22, 135);
    background: linear-gradient(180deg, white 0%, rgba(0, 0, 0, 1) 34%);
  }

  .btn:hover::before {
    bottom: 4px;
    height: 4px;
    background: linear-gradient(180deg, white 0%, rgba(0, 0, 0, 1) 34%);
  }
  .ply {
    background-image: url("./img/play.png");
    width: 170px;
    height: 32px;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
    background-color: transparent;
    animation: play 0.7s infinite;
    max-width: 100%;
    margin: 0 auto;
  }

  @keyframes play {
    from {
      background-color: transparent;
    }
    to {
      background-color: #eb1687;
      background-blend-mode: overlay;
    }
  }

  .welcome {
    max-width: 1024px;
    width: 100%;
    margin: 0 auto;
    height: 100%;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    flex-direction: column;
    background: url("./img/bg.webp") center no-repeat;
    background-size: cover;
  }
  .card-list {
    background-color: transparent;
    width: 200px;
    height: 310px;
    margin: 0 20px 40px;
    border: 1px solid #f1f1f1;
    perspective: 1000px; /* Remove this if you don't want the 3D effect */
  }

  .card {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition-duration: 2s;
    transform-style: preserve-3d;
  }
  .show-back {
    transform: rotateY(180deg);
  }
  .card-front,
  .card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden; /* Safari */
    backface-visibility: hidden;
  }
  /* Style the front side */
  .card-front {
    background-color: yellow;
  }

  /* Style the back side */
  .card-back {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background-color: pink;
    width: 196px;
    height: 300px;
    transform: rotateY(180deg);
  }
  .grid-list {
    display: grid;
    grid-gap: 30px;
    grid-template-columns: repeat(4, 1fr);
  }

  .grid-container {
    align-items: center;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  @media (max-width: 960px) {
    .grid-list {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 400px) {
    .grid-list {
      grid-template-columns: repeat(1, 1fr);
    }
  }
</style>
