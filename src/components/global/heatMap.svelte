<script>
  import { dataset_dev, each } from "svelte/internal";
  import Button from "./button.svelte";

  export let Data = [
    {
      Error: "Error Loading Data",
    },
  ];

  $: areas = Data[0].area ? new Set(Data.map((listing) => listing.area)) : new Set("No Areas");
  $: areasArray = Array.from(areas);

  let uniqueMunicipalities = { error: "no Data" };
  $: {
    uniqueMunicipalities = {};
    Data.forEach(({ area, municipality }) => {
      if (!uniqueMunicipalities[area]) uniqueMunicipalities[area] = [];
      if (!uniqueMunicipalities[area].includes(municipality)) uniqueMunicipalities[area].push(municipality);
    });
    console.log(uniqueMunicipalities);
  }

  let uniqueUnitSizes = [];

  $: {
    uniqueUnitSizes = [];

    if (Data[0].unitSize != undefined) {
      Data.forEach(({ unitSize }) => {
        let indexOfBedroom = unitSize.indexOf(" Bedroom");
        let numberOfBedrooms = indexOfBedroom != -1 ? parseFloat(unitSize.slice(0, indexOfBedroom).trim()) : "Unknown";

        let indexOfBathroom = unitSize.indexOf(" Bathroom");
        let numberOfBathrooms = indexOfBathroom != -1 ? parseFloat(unitSize.slice(indexOfBedroom + 9, indexOfBathroom).trim()) : "Unknown";

        // Check if sizeNum is a valid number
        if (!isNaN(numberOfBedrooms) && !isNaN(numberOfBathrooms)) {
          uniqueUnitSizes.push(`[${numberOfBedrooms}, ${numberOfBathrooms}]`);
        } 
      });

      uniqueUnitSizes = [...new Set(uniqueUnitSizes)];
      console.log(uniqueUnitSizes);
    }
  }

  const areaCounts = {};
  const areaSum = {};

  $: {
    // Initialize areaCounts and areaSum objects for each area in areasArray
    for (let i = 0; i < areasArray.length; i++) {
      areaCounts[areasArray[i]] = 0;
      areaSum[areasArray[i]] = {};
    }

    // Loop through each listing in the data array and increment the count for its area
    for (let i = 0; i < Data.length; i++) {
      const area = Data[i].area;
      const unitSize = Data[i].unitSize;
      const rent = Number(Data[i].rent);

      // Increment number of listings for this area and unit size
      if (unitSize) {
        areaCounts[area]++;
        if (!areaSum[area][unitSize]) {
          areaSum[area][unitSize] = { count: 1, rent: rent };
        } else {
          areaSum[area][unitSize].count++;
          areaSum[area][unitSize].rent += rent;
        }
      }
    }

    console.log(areaCounts);
    console.log(areaSum);
  }
</script>

{#if Data.Error != undefined}
  <p>{Data.Error}</p>
{:else}
  <table>
    <tbody>
      <!--loop over the areas and give a row for each-->
      {#each areasArray as area}
        <tr class="mainRow">
          <td class="leftTitle">
            <table class="tableNested">
              {#if area in uniqueMunicipalities}
                {#each uniqueMunicipalities[area] as municipality}
                  <tr>{municipality}</tr>
                {/each}
              {/if}
            </table>
            <h4>{area}</h4>
          </td>

          {#each uniqueUnitSizes as unitSize}
            <td>
              {#if areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`]}
                <div class="areaInfo">
                  <h4 class="Active">{areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`].count}</h4>
                  <span class="notActive">$ {(areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`].rent / areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`].count).toFixed(0)}<span /> </span>
                </div>
              {:else}
                <div class="areaInfo">
                  <h4 class="Active">0</h4>
                  <span class="notActive">$ 0000</span>
                </div>
              {/if}

              <!--  <table class="municInfo">
                {#if area in uniqueMunicipalities}
                  {#each uniqueMunicipalities[area] as municipality}
                    <tr>
                      {#if areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`]}
                        <div class="areaInfo">
                          <h4>{areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`].count}</h4>
                          <span>$ {areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`].rent / areaSum[area][`${JSON.parse(unitSize)[0]} Bedroom ${JSON.parse(unitSize)[1]} Bathroom`].count}<span /></span>
                        </div>
                      {/if}
                    </tr>
                  {/each}
                {/if}
              </table> -->
            </td>
          {/each}
        </tr>
      {/each}
      <!-- bottom table row-->
      <tr class="mainRow">
        <td class="leftTitle" />
        {#each uniqueUnitSizes as unitSizeObj}
          <td> <h4 class="vertical">{`${JSON.parse(unitSizeObj)[0]} Beds, ${JSON.parse(unitSizeObj)[1]} Bath`}</h4> </td>
        {/each}
      </tr>
    </tbody>
  </table>
{/if}

<style>
  .Active {
    font-size: 12pt;
    color: blue;
    font-weight: 900;
  }
  .notActive {
    font-size: 7pt;
    color: #0050e3;
  }

  .municInfo {
    display: none;
  }
  .tableNested {
    min-height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    opacity: 0;
  }
  td {
    min-width: 8.75%;
  }
  .areaInfo {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  table {
    min-width: 100%;
    min-height: 100%;
  }
table>tbody{
    display:grid;
  grid-template-columns: 1fr;
  grid-template-rows: repeat(5, .855fr);
}
  .mainRow {
    display: flex;
    flex-basis: 20%;
  }

  .mainRow td {
    border: 1px solid black;
  }
  .leftTitle {
    display: flex;
    flex-direction: row;
    align-items: center;
    min-width: 30%;
    max-width: 30%;
  }

  .leftTitle > h4 {
    max-width: 10%;

    writing-mode: vertical-rl;
    font-size: 8pt;
    border-right: 2px solid black;
    border-left: 2px solid black;
    padding: 0 0.2vw;
  }
  .leftTitle > table {
    min-width: 80% !important;
    max-width: 80%;
    font-size: 8pt;
    text-align: center;
  }

  .leftTitle > table > tr {
    border-bottom: 1px solid black;
  }
  .vertical {
    max-width: 25%;
    writing-mode: vertical-rl;
    font-size: 8pt;
  }
  .verticalTitles {
    display: flex;
    align-items: center;
  }
</style>
