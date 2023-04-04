<script>
  //page level varibles
  let liveServerURL = "https://mesn-backend.onrender.com";
  let localServerURL = "http://localhost:5001";

  //change which is commented dependant on where youre working
  //let currentURL = liveServerURL;
  let currentURL = localServerURL;

  // import components to be used on this page
  import Button from "../../components/global/button.svelte";
  import FilterButton from "../../components/global/FilterButton.svelte";
  import Table from "../../components/global/Table.svelte";
  //import data
  import { rentalDataSvelteStore } from "../../../scripts/data-store.js";

  import DataButtonDiv from "../../components/partials/DataButtonDiv.svelte";
  import Modal from "../../components/global/Modal.svelte";
  import InputValue from "../../components/global/InputValue.svelte";
  import InputChecked from "../../components/global/InputChecked.svelte";
  function handleInputChange(event) {
    minPrice = event.target.value;
    maxPrice= event.target.value;
  }
  let isChecked = false;
  let showModal = false;
  let minPrice = "";
  let maxPrice = "";
  let numberOfBedrooms = 2;
  let shortterm = false;
  let middleterm = false;
  let longterm = false;
  let spring = false;
  let summer =false;
  let fall = false;
  let winter = false;
  // declare a varible to hold the data from the fetch
  let result = {};
  //perform fetch and assign the result to the above varible
  async function getData() {
    await fetch(`${currentURL}/rentalData`, {
      method: "GET",
    })
      .then((data) => {
        return data.json();
      })
      .then((rentalListings) => {
        //loop through thr result and console log each obj
        /* for (const listing in rentalListings) {
                    if (Object.hasOwnProperty.call(rentalListings, listing)) {
                        const listingObj = rentalListings[listing];
                        console.log(listingObj);
                    }
                } */
        //assign the rentalListings from the fetch to the global result varible
        result = rentalListings;
      });
  }
  //IFFIE to run at component initialization
  (async function () {
    await getData();
    console.log(result);
    console.log(Object.entries(result));
  })();

  let addSampleRecord = async () => {
    console.log(`fetching...`);
    await fetch(`${currentURL}/rentalData/sample`, {
      method: "post",
    });
  };

  let dataButtonDivHandleClick = async (e) => {
    console.log(e.target);

    if (e.target.id == "add") {
      await addSampleRecord();
    } else {
    }
  };
</script>

<main>
  <!-- <Button buttonColorVar={'--login-button-color'} buttonText={'populateDB'} />
  <Button /> -->

  <section class="buttonSection">
    <!-- Filter Button Starts -->
    <FilterButton
      on:click={() => (showModal = true)}
      buttonId={"filterButton"}
      buttonIconClass={"fa-solid fa-bars"}
      buttonText={"Filter"}
    />
    <Modal bind:showModal>
      <div class="modalContent">
        <div class="cityTown modalDiv">
          <h2>City/Town</h2>
          <FilterButton
            buttonClass={"cityTownButton"}
            buttonText={"Alliston/Bradford"}
          />
          <FilterButton buttonClass={"cityTownButton"} buttonText={"Barrie"} />
          <FilterButton
            buttonClass={"cityTownButton"}
            buttonText={"Collingwood"}
          />
          <FilterButton buttonClass={"cityTownButton"} buttonText={"Midland"} />
          <FilterButton buttonClass={"cityTownButton"} buttonText={"Orillia"} />
        </div>
        <hr />
        <div class="priceRange modalDiv">
          <h2>Price Range</h2>
          <div class="price">
            <div class="minPrice">
              <label for="minprice">From</label>
              <!-- check if bind:value works -->
              <!-- <p>{minPrice || 'stranger'},{maxPrice}!</p> -->
              <InputValue bind:value={minPrice} on:input={handleInputChange} inputPlaceholder={'minimum price'} inputId={'minprice'} size={'15'}/>
             
              
            </div>
            <i class="fa-solid fa-minus" />
            <div class="maxPrice">
              <label for="maxprice">To</label>
              <InputValue bind:value={maxPrice} on:input={handleInputChange} inputPlaceholder={'maximum price'} inputId={'maxprice'} size={'15'}/>
             
            </div>
          </div>
        </div>
        <hr />
        <div class="housingType modalDiv">
          <h2>Housing Type</h2>
          <FilterButton
            buttonClass={"housingTypeButton"}
            buttonIconClass={"fa-solid fa-house"}
            buttonText={"Detached"}
          />
          <FilterButton
            buttonClass={"housingTypeButton"}
            buttonIconClass={"fa-solid fa-city"}
            buttonText={"Attached"}
          />
          <FilterButton
            buttonClass={"housingTypeButton"}
            buttonIconClass={"fa-solid fa-house-chimney"}
            buttonText={"House"}
          />
          <FilterButton
            buttonClass={"housingTypeButton"}
            buttonIconClass={"fa-solid fa-building"}
            buttonText={"Apartment"}
          />
          <FilterButton
            buttonClass={"housingTypeButton"}
            buttonIconClass={"fa-solid fa-stairs"}
            buttonText={"Basement"}
          />
        </div>
        <hr />
        <div class="numberOfBedrooms modalDiv">
          <h2>Number of Bedrooms</h2>
          
          <input
            type="range"
            id="rangeBedrooms"
            bind:value={numberOfBedrooms}
            min="1"
            max="6"
            step="1"
          />
          <h3>
            You are choosing {numberOfBedrooms} bedrooms now.
          </h3>
        </div>
        <hr />
        <div class="typeOfLease modalDiv">
          <h2>Type of Lease</h2>
          <div class="lease">
            <input
              type="checkbox"
              name="leaseTerm"
              bind:checked={shortterm}
              id="shortterm"
            />
            <label for="shortterm" class="leaseLabel">Less than 6 months</label>
            <input
              type="checkbox"
              name="leaseTerm"
              bind:checked={middleterm}
              id="middleterm"
            />
            <label for="middleterm" class="leaseLabel"
              >6 months to 12 months</label
            >
            <input
              type="checkbox"
              name="leaseTerm"
              bind:checked={longterm}
              id="longterm"
            />
            <label for="longterm" class="leaseLabel">Over 1 year</label>
            <input
              type="checkbox"
              name="leaseTerm"
              bind:checked={spring}
              id="spring"
            />
            <label for="spring" class="leaseLabel"
              >Spring (Seasonal Rental)</label
            >
            <input
              type="checkbox"
              name="leaseTerm"
              bind:checked={summer}
              id="summer"
            />
            <label for="summer" class="leaseLabel"
              >Summer (Seasonal Rental)</label
            >
            <input type="checkbox" name="leaseTerm" bind:checked={fall} id="fall" />
            <label for="fall" class="leaseLabel">Fall (Seasonal Rental)</label>
            <input
              type="checkbox"
              name="leaseTerm"
              bind:checked={winter}
              id="winter"
            />
            <label for="winter" class="leaseLabel"
              >Winter (Seasonal Rental)</label
            >
          </div>
        </div>
      </div>
    </Modal>
    <!-- Filter Button Ends -->

    <div class="dropdown">
      <button
        class="dropdown-toggle"
        type="button"
        data-bs-toggle="dropdown"
        aria-expanded="false"
      >
        Categories
      </button>
      <ul class="dropdown-menu">
        <li><a class="dropdown-item" href="#">City/Town</a></li>

        <li><a class="dropdown-item" href="#">Price</a></li>

        <li><a class="dropdown-item" href="#">Housing Type</a></li>
        <li>
          <a class="dropdown-item" href="#">Number of bedrooms</a>
        </li>
        <li><a class="dropdown-item" href="#">Type of Lease</a></li>
      </ul>
    </div>
    <DataButtonDiv on:click={dataButtonDivHandleClick} />
  </section>
  <!-- table -->
  {#if Object.entries(result).length > 0}
    <Table tableData={result} />
  {:else}
    <Table />
  {/if}
</main>

<style>
  header {
    justify-content: space-between;
    border: solid white 3px;
  }

  /* toggle button */

  .toggle {
    margin: 0.6em 4em 0 0;
    position: relative;
    width: 55px;
    height: 28px;
    border-radius: 30px;
    overflow: hidden;
    cursor: pointer;
  }

  .toggle:before {
    content: "";
    height: 100%;
    display: block;
    background: darkgray;
  }

  .toggle:after {
    content: "";
    position: absolute;
    top: 3px;
    left: 3px;
    width: 19px;
    height: 22px;
    border-radius: 30px;
    background: #fff;
    transition: 0.2s ease-out;
  }

  .toggle.checked:before {
    background: #35c759;
  }

  .toggle.checked:after {
    left: 33px;
  }

  /* body */

  .buttonSection {
    height: 80px;
    background-color: #f0f0f0;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    padding: 0 2vw;
  }

  /* Modal Dialoge */
  .modalDiv {
    padding: 10px 20px;
  }
  .modalContent h2 {
    margin: 10px;
    font-size: 23px;
  }
  .modalContent h3,
  .modalContent label,
  .modalContent div label {
    margin: 10px;
    font-size: 17px;
  }
  .lease {
    display: grid;
    grid-template-columns: 3% 53% 3% 41%;
    margin: 10px;
  }

  .leaseLabel {
    font-weight: normal;
    font-size: 17px;
    margin: 0;
  }
  #rangeBedrooms {
    width: 100%;
    margin: 10px;
  }
  #shortterm,
  #middleterm,
  #longterm,
  #spring,
  #summer,
  #fall,
  #winter {
    width: 20px;
    margin: 0;
  }

  .fa-minus {
    margin: 0 1em;
  }

  .minPrice,
  .maxPrice {
    display: inline;
    font-weight: 400;
  }

  
  button {
    background-color: rgb(190, 190, 190);
    border: none;
    border-radius: 10px;
    cursor: pointer;
  }

  /* dropdown menu */

  .dropdown {
    border-radius: 10px;
    background-color: rgb(190, 190, 190);
    padding: 0.1em;
  }

  /* Table */

  table {
    border-collapse: collapse;
    border-spacing: 0;
    width: 95vw;
    margin: 1em 0 0 2.5em;
  }

  table tr {
    border-bottom: solid 1px #eee;
  }

  table th,
  table td {
    text-align: center;
    padding: 15px 0;
  }

  table tr:nth-child(odd) {
    background: #e9faf9;
  }

  table th {
    background-color: skyblue;
  }
</style>
