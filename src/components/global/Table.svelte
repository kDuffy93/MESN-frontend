<!-- js -->
<script>
  export let tableClass;
  export let tableId;

  export let tableData = [
    {
      ListingNo: '',
      StratifiedArea: '',
      Municipality: '',
      StreetNo: '',
      StreetName: '',
      HousingType: 'loading...',
      UnitSize: '',
      SecondarySuite: '',
      MonthlyRent: '',
      UtilitiesIncluded: '',
      LandlordType: '',
      Stability: '',
    },
  ];
</script>

<!-- reference link: https://italo-silva.medium.com/svelte-how-to-create-a-dynamic-table-component-1c7d33a307e3 -->

<!-- html -->
<table id={tableId} class={tableClass}>
  <thead>
    <tr>
      {#each Object.keys(tableData[0]) as columnHeading}
        <th>{columnHeading}</th>
      {/each}
    </tr>
  </thead>
  <tbody>
    {#each Object.values(tableData) as row}
      <tr>
        {#each Object.values(row) as cell}
          <td>{cell}</td>
        {/each}
      </tr>
    {/each}
  </tbody>
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
