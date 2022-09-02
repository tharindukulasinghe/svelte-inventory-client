<script context="module">
  export async function preload() {
    let res = await this.fetch(`http://localhost:5197/api/Repair`);
    const repairs = await res.json();
    return { repairs };
  }
</script>

<script>
  export let repairs = [];

  const getStatusText = (status) => {
    switch (status) {
      case 0:
        return "Open";
      case 1:
        return "Fixed";
      case 2:
        return "Delivered";
      case 3:
        return "Unfixable";
      default:
        return "Open";
    }
  };

  const getStatusClass = (status) => {
    switch (status) {
      case 0:
        return "text-bg-warning";
      case 1:
        return "text-bg-success";
      case 2:
        return "text-bg-info";
      case 3:
        return "text-bg-danger";
      default:
        return "text-bg-warning";
    }
  };

  const getFormattedFee = (fee) => {
    if (fee === 0) {
      return "";
    } else {
      return "$" + (Math.round(fee * 100) / 100).toFixed(2);
    }
  };
</script>

<div>
  <div class="container">
    <h1>Inventory</h1>
    <table class="table table-hover">
      <thead>
        <tr>
          <th scope="col">Item Name</th>
          <th scope="col">Item Code</th>
          <th scope="col">Telephone No</th>
          <th scope="col">Issue</th>
          <th scope="col">Status</th>
          <th scope="col" class="number">Fee</th>
          <th scope="col" />
        </tr>
      </thead>
      <tbody>
        {#each repairs as repair}
          <tr>
            <td>{repair.item.itemName}</td>
            <td>{repair.item.itemCode}</td>
            <td>{repair.contactNo}</td>
            <td>{repair.issue}</td>
            <td
              ><span class="badge {getStatusClass(repair.status)}"
                >{getStatusText(repair.status)}</span
              ></td
            >
            <td class="number">{getFormattedFee(repair.fee)}</td>
            <td
              ><a class="btn btn-primary btn-sm" href="inventory/{repair.id}"
                >Update</a
              ></td
            >
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</div>

<style>
</style>
