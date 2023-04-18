<!-- js -->
<script>
  export let tableClass;
  export let tableId;

  export let tableData = [];
  let formattedTableData;
  $: {
    formattedTableData = [];
    tableData.forEach((listing) => {
      let tempObject = {
        Address: {
          "Street Address": listing.address != undefined ? listing.address : "Unknown",
          Area: listing.area != undefined ? listing.area : "Unknown",
          Municipality: listing.municipality != undefined ? listing.municipality : "Unknown",
          "Geo-Location": listing.geolocation != undefined ? listing.geolocation : "Unknown",
        },
        Rent: {
          Price: listing.rent != undefined ? listing.rent : "Unknown",
          Frequency: listing.rentFrequency != undefined ? listing.rentFrequency : "Unknown",
        },
        "Unit Size": listing.unitSize != undefined ? listing.unitSize : "Unknown",
        Description: listing.description != undefined ? listing.description : "Unknown",
        Utilities: {
          Included: listing.utilitiesIncluded != undefined ? listing.utilitiesIncluded : "Unknown",
          Additional: listing.utilitiesAdditional != undefined ? listing.utilitiesAdditional : "Unknown",
        },
        Available: listing.avaibility != undefined ? listing.avaibility : "Unknown",
      };
      formattedTableData.push(tempObject);
    });
  }
</script>

<!-- reference link: https://italo-silva.medium.com/svelte-how-to-create-a-dynamic-table-component-1c7d33a307e3 -->

<!-- html -->
<table id={tableId} class={tableClass}>
  {#if formattedTableData.length > 0}
    <thead>
      <tr>
        <!-- <th>Record No.</th> -->
        <th>No.</th>
        {#each Object.keys(formattedTableData[0]) as columnHeading}
          <th>{columnHeading}</th>
        {/each}
      </tr>
    </thead>
    <tbody>
      {#each Object.values(formattedTableData) as row, i}
        <tr class="MainTableRow">
          <td class="odd">{i + 1}</td>
          {#each Object.entries(row) as [key, cell], iterator}
            {#if cell}
              {#if typeof cell == typeof {}}
                {#if iterator % 2 == 0}<td class="even">
                    <div class="objectCell {key}">
                      {#each Object.keys(cell) as nestedKey, i}
                        <div>
                          <label for="{String(nestedKey)}{i}">{nestedKey}</label>
                          {#each Object.values(cell) as nestedValue, i2}
                            {#if i == i2}
                              {#if nestedKey == "Geo-Location"}
                                <a title="Open in Google Maps" id="{String(nestedValue)}{i2}" href={`https://www.google.ca/maps/@${nestedValue},21z`}><i class="fa-solid fa-map-location-dot" /></a>
                              {:else if nestedKey == "Additional"}
                                {#if nestedValue.length == 0}
                                  <div class="empty">
                                    {#if nestedValue.includes("Plus Water")}
                                      <i title="Plus Water" class="fa-solid fa-shower waterIcon" />{/if}
                                    {#if nestedValue.includes("Plus Heat")}
                                      <i title="Plus Heat" class="fa-solid fa-fire-burner heatIcon" />{/if}
                                    {#if nestedValue.includes("Plus Hydro")}
                                      <i title="Plus Hydro" class="fa-solid fa-bolt hydroIcon" />{/if}
                                  </div>
                                {:else}
                                  <div>
                                    {#if nestedValue.includes("Plus Water")}
                                      <i title="Plus Water" class="fa-solid fa-shower waterIcon" />{/if}
                                    {#if nestedValue.includes("Plus Heat")}
                                      <i title="Plus Heat" class="fa-solid fa-fire-burner heatIcon" />{/if}
                                    {#if nestedValue.includes("Plus Hydro")}
                                      <i title="Plus Hydro" class="fa-solid fa-bolt hydroIcon" />{/if}
                                  </div>
                                {/if}
                              {:else if nestedKey == "Included"}
                                {#if nestedValue == "Yes"}
                                  <div><i class="fa-solid fa-thumbs-up yesIcon" /></div>
                                {:else}
                                  <div>
                                    <i class="fa-solid fa-thumbs-down noIcon" />
                                  </div>{/if}
                              {:else}
                                <p id="{String(nestedValue)}{i2}">{nestedValue}</p>
                              {/if}
                            {/if}
                          {/each}
                        </div>
                      {/each}
                    </div>
                  </td>
                {:else}
                  <td class="odd">
                    <div class="objectCell">
                      {#each Object.keys(cell) as nestedKey, i}
                        <div>
                          <label for="{String(nestedKey)}{i}">{nestedKey}</label>
                          {#each Object.values(cell) as nestedValue, i2}
                            {#if i == i2}
                              {#if nestedKey == "Geo-Location"}
                                <a title="Open in Google Maps" id="{String(nestedValue)}{i2}" href={`https://www.google.ca/maps/@${nestedValue},21z`}><i class="fa-solid fa-map-location-dot" /></a>
                              {:else if nestedKey == "Additional"}
                                <div>
                                  {#if nestedValue.includes("Plus Water")}
                                    <i title="Plus Water" class="fa-solid fa-shower waterIcon" />{/if}
                                  {#if nestedValue.includes("Plus Heat")}
                                    <i title="Plus Heat" class="fa-solid fa-fire-burner heatIcon" />{/if}
                                  {#if nestedValue.includes("Plus Hydro")}
                                    <i title="Plus Hydro" class="fa-solid fa-bolt hydroIcon" />{/if}
                                </div>
                              {:else}
                                <p id="{String(nestedValue)}{i2}">{nestedValue}</p>
                              {/if}
                            {/if}
                          {/each}
                        </div>
                      {/each}
                    </div>
                  </td>
                {/if}
              {:else if typeof cell == typeof ""}
                {#if iterator % 2 == 0}
                  {#if key == "Description"}
                    <td class="description even"><p>{cell}</p></td>
                  {:else}
                    <td class="even">{cell}</td>
                  {/if}
                {:else if key == "Description"}
                  <td class="description odd"><p>{cell}</p></td>
                {:else}
                  <td class="odd">{cell}</td>
                {/if}
              {:else}
                <td />
              {/if}
            {:else}
              <td />
            {/if}
          {/each}
        </tr>
      {/each}
    </tbody>
  {:else}<thead>
      <tr><th>loading...</th></tr>
    </thead><tbody>
      <tr><td>loading...</td></tr>
    </tbody>
  {/if}
</table>

<!-- css -->
<style>
  :has(> .empty) {
    display: none;
  }
  .waterIcon {
    color: #337ab7;
  }
  .heatIcon {
    color: rgba(255, 123, 0, 0.856);
  }
  .hydroIcon {
    color: goldenrod;
  }
  .noIcon {
    color: rgba(255, 0, 0, 0.718);
  }
  .yesIcon {
    color: rgba(0, 128, 0, 0.801);
  }
  i {
    font-size: 22pt;
    margin: 7.5px 5px 0 0;
  }

  .even {
    /* background-color: #93b18c25; */
  }

  .odd {
    background-color: #3a9ef625;
  }

  .MainTableRow {
    height: 150px;
  }

  .description > p {
    max-height: 128px;
    overflow-y: scroll;
  }

  .MainTableRow > td {
    width: 12.5%;
  }
  .MainTableRow > td:first-of-type {
    width: 2.5%;
  }
  .MainTableRow > .description {
    width: 30%;
    text-align: center;
  }
  :has(.objectCell) {
  }
  .objectCell {
    padding: 2% 0;
    display: grid;
    grid-template-rows: 1fr 1fr;
    grid-row-gap: 10px;
    justify-content: center;
    align-items: center;
  }

  .Address {
    grid-template-columns: 1fr 1fr;
  }

  .objectCell > div {
  }
  .objectCell > div > label {
  }

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  table {
    height: fit-content;
    border-spacing: 1;
    border-collapse: collapse;
    background: #fff;
    border-radius: 10px;
    overflow: hidden;
    width: 87.5vw;
    margin: 5vh auto;
    position: relative;
    margin-right: 4vw;
  }

  table td,
  table th {
    padding: 10px;
  }

  table thead tr {
    height: 60px;
    background: #00539be3;
  }

  table tbody tr {
    max-height: 50px;
    overflow-y: hidden;
  }
  table tbody tr:last-child {
    border: 0;
  }
  table td,
  table th {
    text-align: center;
  }

  table thead tr th {
    font-family: OpenSans-Regular;
    font-size: 18px;
    color: #fff;
    line-height: 1.2;
    font-weight: unset;
  }

  tbody tr:nth-child(even) {
    background-color: #f5f5f5;
  }

  tbody tr {
    font-family: OpenSans-Regular;
    font-size: 15px;
    color: gray;
    line-height: 1.2;
    font-weight: unset;
  }

  tbody tr:hover {
    color: #555;
    background-color: #f5f5f5;
    cursor: pointer;
  }

  div.objectCell div:nth-child(4) a {
    word-wrap: break-word;
  }
</style>
