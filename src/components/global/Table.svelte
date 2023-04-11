<!-- js -->
<script>
  export let tableClass;
  export let tableId;

  export let tableData = [
    {
      Address: {
        "Street Address": "",
        Area: "",
        Municipality: "",
        "Geo-Location": "",
      },
      Rent: {
        Price: `$0`,
        Frequency: "",
      },
      UnitSize: "",
      Description: "",
      Utilities: {
        Included: "",
        Additional: "",
      },
      Available: "",
    },
  ];
  let formattedTableData;
  $: {
    formattedTableData = [];
    tableData.forEach((listing) => {
      let tempObject = {
        Address: {
          "Street Address": listing.address != undefined ? listing.address : "Unknown",
          Area: listing.StratifiedAreas != undefined ? listing.StratifiedAreas : "Unknown",
          Municipality: listing.Municipalities != undefined ? listing.Municipalities : "Unknown",
          "Geo-Location": listing.geolocation != undefined ? listing.geolocation : "Unknown",
        },
        Rent: {
          Price: listing.rent != undefined ? listing.rent : "Unknown",
          Frequency: listing.rentFrequency != undefined ?  listing.rentFrequency : "Unknown",
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
        <th>Record No.</th>
        {#each Object.keys(formattedTableData[0]) as columnHeading}
          <th>{columnHeading}</th>
        {/each}
      </tr>
    </thead>
    <tbody>
      {#each Object.values(formattedTableData) as row, i}
        <tr>
          <td>{i + 1}</td>
          {#each Object.values(row) as cell}
            {#if cell}
              {#if typeof cell == typeof {}}
                <td>
                  {#each Object.keys(cell) as nestedKey, i}
                    <div>
                      <label for="{String(nestedKey)}{i}">{nestedKey}</label>
                      {#each Object.values(cell) as nestedValue, i2}
                        {#if i == i2}
                          <p id="{String(nestedValue)}{i2}">{nestedValue}</p>
                        {/if}
                      {/each}
                    </div>
                  {/each}
                </td>
              {:else if typeof cell == typeof ""}
                <td>{cell}</td>
              {:else}
                <td />
              {/if}
              {:else}
              <td></td>
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
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  table {
    border-spacing: 1;
    border-collapse: collapse;
    background: #fff;
    border-radius: 10px;
    overflow: hidden;
    width: 95vw;
    margin: 5vh auto;
    position: relative;
  }

  table td,
  table th {
    padding-left: 8px;
  }

  table thead tr {
    height: 60px;
    background: #36304a;
  }

  table tbody tr {
    height: 50px;
  }
  table tbody tr:last-child {
    border: 0;
  }

  table td,
  table th {
    text-align: left;
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
</style>
