<script>
  import HeatToggle from "../../components/global/heatToggle.svelte";
  import HeatMap from "../../components/global/heatMap.svelte";
  //page level varibles
  let liveServerURL = "https://mesn-backend.onrender.com";
  let localServerURL = "http://localhost:5001";

  //change which is commented dependant on where youre working
  //let currentURL = liveServerURL;
  let currentURL = localServerURL;

  let result = {};
  async function getData() {
    await fetch(`${currentURL}/heatMap`, {
      method: "GET",
    })
      .then((data) => {
        return data.json();
      })
      .then(async (rentalListings) => {
        let temparray = [];
        await rentalListings.forEach((listing) => {
          temparray.push(JSON.parse(listing));
        });
        result = temparray;
      });
  }
  //IFFIE to run at component initialization
  (async function () {
    await getData();
    console.log(result);
  })();
</script>

<main class="container">
  <div>
    {#if Object.entries(result).length > 0}
      <HeatMap Data={result} />
    {:else}
      <HeatMap />
    {/if}
  </div>
  <aside>
    <h2>Filter By</h2>
    <div>
      <label id="noUnits">Total Listings</label>
      <div>
        <HeatToggle heatId={"slider"} class="heatToggle" heatClass={"switch"} heatToggleType={"checkbox"} heatSpanClassOne={"slider round one"} heatSpanClassTwo={"slider round two"} />
      </div>
      <label id="avgRent">Average Rent</label>
    </div>
  </aside>
</main>

<style>




  main {
    display: flex;
  }
  main > div {
    background-color: #f6f6f6;
    width: 60%;
    height: 70vh;
    margin-top: 2.5vh;
    margin-left: 15%;

  }
  main > aside {
    height: 100%;
    width: 33%;
    padding-top: 2.5vh;
    padding-left: 1vw;
  }
  main > aside > h2 {
    font-size: smaller;
    text-decoration: underline;
    text-align: center;
  }
  main > aside > div {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    padding-top: 10%;
  }
  main > aside > div > div {
  }
  main > aside > div > label {
    width: 30%;
  }

  #noUnits {
    margin-right: -15%;
    font-size: smaller;
    color: #c5e0ee;
  }
  #avgRent {
    margin-left: -7.5%;

    font-size: smaller;
    color: #ade498;
  }

  main > div > li {
    list-style: none;
    text-align: center;
    padding-top: 1.5vh;
    border: 0.5px solid black;
  }

  main > div > li > p:nth-of-type(2) {
    font-size: 50%;
  }

  main > div > li > p {
    font-weight: bolder;
  }

  .vertical {
    writing-mode: vertical-lr;
    text-orientation: upright;

    background-color: #f6f6f6;
  }

  .filter {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(5, 1fr);
    grid-template-areas:
      "area ."
      "area ."
      "area type"
      ". type"
      ". type"
      ". type";
    padding: 0;
  }

  .filter > div:nth-of-type(1) {
    grid-area: area;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
  }

  .filter > div:nth-of-type(2) {
    grid-area: type;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
  }

  label {
    text-align: left;
    width: 75%;
  }

  .black {
    background-color: black;
  }
  .offWhite {
    background-color: #f6f6f6;
  }
  .border3pxblack {
    border: 3px solid black;
  }


  /* -- slider css --*/
  .switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
  }

  /* Hide default HTML checkbox */
  .switch input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  /* The slider */
  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: lightgreen;
    -webkit-transition: 0.4s;
    transition: 0.4s;
  }

  .slider:before {
    position: absolute;
    content: "";
    height: 26px;
    width: 26px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: 0.4s;
    transition: 0.4s;
  }

  input:checked + .slider {
    background-color: #2196f3;
  }

  input:focus + .slider {
    box-shadow: 0 0 1px #2196f3;
  }

  input:checked + .slider:before {
    -webkit-transform: translateX(26px);
    -ms-transform: translateX(26px);
    transform: translateX(26px);
  }

  /* Rounded sliders */
  .slider.round {
    border-radius: 34px;
  }

  .slider.round:before {
    border-radius: 50%;
  }
</style>
