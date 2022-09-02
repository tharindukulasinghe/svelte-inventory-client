<script context="module">
  export async function preload() {
    let res = await this.fetch(`http://localhost:5197/api/Repair/Summary`);
    const summary = await res.json();
    return { summary };
  }
</script>

<script>
  export let summary = [];

  const getFormattedTotal = (charge) => {
    if (charge === 0) {
      return "";
    } else {
      return "$" + (Math.round(charge * 100) / 100).toFixed(2);
    }
  };
</script>

<div>
  <div class="container">
    <h1>Summary</h1>
    <table class="table table-hover">
      <thead>
        <tr>
          <th scope="col">Item Code</th>
          <th scope="col">Item Name</th>
          <th scope="col" class="number">Count</th>
          <th scope="col" class="number">Total Charge</th>
        </tr>
      </thead>
      <tbody>
        {#each summary as item}
          <tr>
            <td>{item.itemCode}</td>
            <td>{item.itemName}</td>
            <td class="number">{item.count}</td>
            <td class="number">{getFormattedTotal(item.totalCharge)}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</div>

<style>
</style>
