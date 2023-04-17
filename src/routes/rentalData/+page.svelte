<script>
  import { ExportToCsv } from "export-to-csv";
  //page level varibles
  let liveServerURL = "https://mesn-backend.onrender.com";
  let localServerURL = "http://localhost:5001";

  //change which is commented dependant on where youre working
  let currentURL = liveServerURL;
  //let currentURL = localServerURL;

  // import components to be used on this page
  import Button from "../../components/global/button.svelte";
  import FilterButton from "../../components/global/FilterButton.svelte";
  import Table from "../../components/global/Table.svelte";
  //import data

  import DataButtonDiv from "../../components/partials/DataButtonDiv.svelte";
  import Modal from "../../components/global/Modal.svelte";
  import InputValue from "../../components/global/InputValue.svelte";
  import InputChecked from "../../components/global/InputChecked.svelte";

  let priceFilters = {
    minPrice: "",
    maxPrice: "",
  };

  let activeFilters = {
    leaseType: [],
    housingType: [],
    numberOfBedrooms: {
      number: 2,
      active: false,
    },
    price: {
      priceMinimum: 0,
      priceMaximum: 0,
      active: false,
    },
    area: [],
  };

  let leaseTypeFilters = {
    shortTerm: "Less Than 6 Months",
    middleTerm: "6 Months To 1 Year",
    longTerm: "Over 1 Year",
    spring: "Seasonal (Spring)",
    summer: "Seasonal (Summer)",
    fall: "Seasonal (Fall)",
    winter: "Seasonal (Winter)",
  };

  let cityFilters = {
    bradford: "Alliston/Bradford",
    barrie: "Barrie",
    collingwood: "Collingwood",
    midland: "Midland",
    orillia: "Orillia",
  };

  let housingFilters = {
    Detached: "fa-solid fa-house",
    Attached: "fa-solid fa-city",
    House: "fa-solid fa-house-chimney",
    Apartment: "fa-solid fa-building",
    Basement: "fa-solid fa-stairs",
  };

  const housingFiltersArray = Object.entries(housingFilters).map(([key, value]) => ({ key, value }));
  const cityFiltersArray = Object.entries(cityFilters).map(([key, value]) => ({ key, value }));
  const leaseTypeFiltersArray = Object.entries(leaseTypeFilters).map(([key, value]) => ({ key, value }));

  let showModal = false;

  const options = {
    fieldSeparator: ",",
    quoteStrings: '"',
    decimalSeparator: ".",
    showLabels: false,
    showTitle: false,
    title: `${Date.now()}-AllRentalListings`,
    filename: `${Date.now()}-AllRentalListings`,
    useTextFile: false,
    useBom: true,
    useKeysAsHeaders: true,
  };
  const csvExporter = new ExportToCsv(options);
  let exportObject = [];

  // declare a varible to hold the data from the fetch
  let result = {};

  let filteredTableData = [];

  let activeFilterscopy = {
    leaseType: [],
    housingType: [],
    numberOfBedrooms: {
      number: 2,
      active: false,
    },
    price: {
      priceMinimum: 0,
      priceMaximum: 0,
      active: false,
    },
    area: [],
  };

  $: {
    try {
      filteredTableData = [];

      result.forEach((listing) => {
        console.log(listing);
        let ok = true;
        // check if this listing adheres to the current filters. If it does, Push to filteredTableData - if not, dont.

        // this checks if the area of the listing were currently on is in the list of active filters. if its now set ok to false
        let matchedAny = false;

        if (activeFilters.area.length > 0) {
          activeFilters.area.forEach((area) => {
            console.log(`ActiveFilterarea: ${area} | listing.area: ${listing.area} `)
            if (area.includes(listing.area.toLowerCase())) {
              matchedAny = true;
            } else {
            }
          });
        } else {
          matchedAny = true;
        }

        // this checks if the number of bedrooms of the listing were currently on is bigger than the number of bedrooms set in the filter if the checkbox is checked.
        // if it is set ok to false

        let tooManyBedrooms = false;

        if (activeFilters.numberOfBedrooms.active == true) {
          if (Number(listing.bedrooms) > Number(activeFilters.numberOfBedrooms.number)) {
            console.log(`Too many bedrooms`);
            tooManyBedrooms = true;
          }
        }
        
       
        // this checks if the listing's rent is between the minimum and maximum prices set in the activeFilters object if the checkbox is checked
        // if its not, set ok to false

         let inRange = true;
        if (activeFilters.price.active == true) {
          if (listing.rent < activeFilters.price.priceMinimum && activeFilters.price.priceMinimun !== 0 && activeFilters.price.priceMinimum!== undefined) {
            console.log(`Rent too low`);
            inRange = false;
          } else if (listing.rent > activeFilters.price.priceMaximum && activeFilters.price.priceMaximum !== 0 && activeFilters.price.priceMaximum !== undefined) {
            console.log(`Rent too High`);
            inRange = false;
          }
        } 


         if (!matchedAny) {
          ok = false;
        }
        if(tooManyBedrooms){
          ok = false;
        }
        if(!inRange){
          ok = false;
        }
        if (ok) {
          filteredTableData.push(listing);
        }
      });
    } catch {
      console.log("result is not an array yet");
    }
  }

  //perform fetch and assign the result to the above varible
  async function getData() {
    await fetch(`${currentURL}/rentalData`, {
      method: "GET",
    })
      .then((data) => {
        return data.json();
      })
      .then(async (rentalListings) => {
        //loop through thr result and console log each obj
        /* for (const listing in rentalListings) {
                    if (Object.hasOwnProperty.call(rentalListings, listing)) {
                        const listingObj = rentalListings[listing];
                        console.log(listingObj);
                    }
                } */
        //assign the rentalListings from the fetch to the global result varible
        let temparray = [];

        try {
          await rentalListings.forEach((listing) => {
            temparray.push(JSON.parse(listing));
          });
        } catch {
          for (const rentalisting in rentalListings) {
            if (Object.hasOwnProperty.call(rentalListings, rentalisting)) {
              const listing = rentalListings[rentalisting];
              temparray.push(JSON.parse(JSON.stringify(listing)));
            }
          }
        }
        console.log(temparray);
        result = temparray;
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
    if (e.target.id == "add") {
      await addSampleRecord();
    } else if (e.target.id == "all") {
      await exportToCSV(result);
    } else if (e.target.id == "current") {
      await exportToCSV(filteredTableData);
    }
  };

  let exportToCSV = async (objectToExport) => {
    console.log(`exporting...`);
    exportObject = [];

    objectToExport.forEach((element) => {
      let tempObject = {
        Source: element.collectedFrom,
        "Date Collected": element.dateCollected,
        "Stratified Area": element.area,
        "Local Municipality": element.municipality,
        Address: element.address,
        Geolocation: element.geolocation,
        Bedrooms: element.bedrooms,
        "Monthly Rent": element.rent,
        "Payment Interval": element.rentFrequency,
        "Utilities Included": element.utilitiesIncluded,
        // "Utilities Additional": element.utilitiesAdditional,
        Avaibility: element.avaibility,
      };
      exportObject.push(tempObject);
    });
    csvExporter.generateCsv(exportObject);
    console.log(exportObject);
  };

  let cityButtonClick = async (e) => {
    let buttonID = e.target.id;
    if (activeFilters.area.includes(buttonID)) {
      let indexOfObjToRemove = activeFilters.area.indexOf(buttonID);
      activeFilters.area.splice(indexOfObjToRemove, 1);
      activeFilters = activeFilters;
    } else {
      activeFilters.area.push(buttonID);
      activeFilters = activeFilters;
    }
    console.log(activeFilters.area);
  };

  let housingButtonClick = async (e) => {
    let buttonID = e.target.id;
    if (activeFilters.housingType.includes(buttonID)) {
      let indexOfObjToRemove = activeFilters.housingType.indexOf(buttonID);
      activeFilters.housingType.splice(indexOfObjToRemove, 1);
      activeFilters = activeFilters;
    } else {
      activeFilters.housingType.push(buttonID);
      activeFilters = activeFilters;
    }
    console.log(activeFilters.area);
  };

  let handleInputChange = async (e) => {
    let inputId = e.target.id;
    if (inputId == "minprice") {
      activeFilters.price.priceMinimum = e.target.value;
    } else {
      activeFilters.price.priceMaximum = e.target.value;
    }
    console.log(activeFilters.price);
  };
</script>

<main>
  <!-- <Button buttonColorVar={'--login-button-color'} buttonText={'populateDB'} />
  <Button /> -->

  <section class="buttonSection">
    <!-- Filter Button Starts -->
    <FilterButton class="filterButton" on:click={() => (showModal = true)} buttonId={"filterButton"} buttonIconClass={"fa-solid fa-bars"} buttonText={"Filter"} />
    <Modal bind:showModal>
      <div class="modalContent">
        <div class="cityTown modalDiv">
          <h2>City/Town</h2>
          {#each cityFiltersArray as cityFilter}
            {#if activeFilters.area.includes(cityFilter.key)}
              <FilterButton on:click={cityButtonClick} value={cityFilter.key} buttonClass={"cityTownButton active"} buttonId={cityFilter.key} buttonText={cityFilter.value} />
            {:else}
              <FilterButton on:click={cityButtonClick} value={cityFilter.key} buttonClass={"cityTownButton"} buttonId={cityFilter.key} buttonText={cityFilter.value} />
            {/if}
          {/each}
        </div>
        <hr />
        <div class="priceRange modalDiv">
          <h2>Price Range</h2>

          <div class="price">
            <input type="checkbox" class="toggleFilterInput" id="filterByPriceToggle" bind:checked={activeFilters.price.active} />
            <div class="minPrice">
              <label for="minprice">From</label>
              <!-- check if bind:value works -->
              <!-- <p>{minPrice || 'stranger'},{maxPrice}!</p> -->
              <InputValue bind:value={priceFilters.minPrice} on:input={handleInputChange} inputPlaceholder={"minimum price"} inputId={"minprice"} size={"15"} />
            </div>
            <i class="fa-solid fa-minus" />
            <div class="maxPrice">
              <label for="maxprice">To</label>
              <InputValue bind:value={priceFilters.maxPrice} on:input={handleInputChange} inputPlaceholder={"maximum price"} inputId={"maxprice"} size={"15"} />
            </div>
          </div>
        </div>
        <hr />
        <div class="housingType modalDiv">
          <h2>Housing Type</h2>

          {#each housingFiltersArray as housingFilter}
            {#if activeFilters.housingType.includes(housingFilter.key)}
              <FilterButton on:click={housingButtonClick} value={housingFilter.key} buttonIconClass={housingFilter.value} buttonClass={"housingTypeButton active"} buttonId={housingFilter.key} buttonText={housingFilter.key} />
            {:else}
              <FilterButton on:click={housingButtonClick} value={housingFilter.key} buttonIconClass={housingFilter.value} buttonClass={"housingTypeButton"} buttonId={housingFilter.key} buttonText={housingFilter.key} />
            {/if}
          {/each}
        </div>
        <hr />
        <div class="numberOfBedrooms modalDiv">
          <h2>Number of Bedrooms</h2>
          <div class="filterToggleRow">
            <input class="toggleFilterInput" type="checkbox" id="filterByBedroomsToggle" bind:checked={activeFilters.numberOfBedrooms.active} />
            <input type="range" id="rangeBedrooms" bind:value={activeFilters.numberOfBedrooms.number} min="1" max="6" step="1" />
          </div>
          <h3>You are choosing {activeFilters.numberOfBedrooms.number} bedrooms now.</h3>
        </div>
        <hr />
        <div class="typeOfLease modalDiv">
          <h2>Type of Lease</h2>
          <div class="lease">
            {#each leaseTypeFiltersArray as leasetype}
              <label class="leaseLabel">
                <input type="checkbox" bind:group={activeFilters.leaseType} name="leaseTerm" value={leasetype.key} />
                {leasetype.value}
                {console.log(activeFilters)}
              </label>
            {/each}
          </div>
        </div>
      </div>
    </Modal>
    <!-- Filter Button Ends -->

    <DataButtonDiv on:click={dataButtonDivHandleClick} />
  </section>
  <!-- table -->
  {#if Object.entries(result).length > 0}
    <Table class="table" tableData={filteredTableData} />
  {:else}
    <Table />
  {/if}
</main>

<style>
  main{
    display:flex;
  }
.table{
  margin-right:2vw;
}
  .housingType,
  .typeOfLease {
    pointer-events: none;
    opacity: 35%;
  }
  #filterByBedroomsToggle {
    margin: 0;
  }
  #rangeBedrooms {
    width: 85%;
    display: unset;
    margin-bottom: -5px;
  }

  .numberOfBedrooms > h3 {
    text-align: center;
  }

  .toggleFilterInput {
    width: 10%;
    transform: scale(2);
  }

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
    height: 80vh;
    background-color: rgba(0, 0, 0, 0);
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-evenly;
    align-items: center;
    padding: 0 2vw;
    position:sticky;
    top: 7.5px;
    z-index: 100;
    flex-direction: column;
    max-width: 5%;
    margin: 2vw;
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
    grid-template-columns: repeat(3, 33%);
    margin: 10px;
  }

  .leaseLabel {
    font-weight: normal;
    font-size: 17px;
    margin: 0;
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
