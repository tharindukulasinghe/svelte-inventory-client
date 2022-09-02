<script context="module">
  export async function preload() {
    let res = await this.fetch(`http://localhost:5197/api/Item`);
    const items = await res.json();
    return { items };
  }
</script>

<script>
  export let items = [];
</script>

<div>
  <div class="container">
    <h1>Items</h1>
    <table class="table table-hover">
      <thead>
        <tr>
          <th scope="col">Item Name</th>
          <th scope="col">Item Code</th>
        </tr>
      </thead>
      <tbody>
        {#each items as item}
          <tr>
            <td>{item.itemName}</td>
            <td>{item.itemCode}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</div>

<style>
</style>
