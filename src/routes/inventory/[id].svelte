<script context="module">
  export async function preload(page, session) {
    const { id } = page.params;
    const res = await this.fetch(`http://localhost:5197/api/Repair/${id}`);
    const repair = await res.json();
    return { repair };
  }
</script>

<script>
  import { goto } from "@sapper/app";
  export let repair;

  $: isFormInvalid = repair.fee == null || repair.fee == 0;

  const handleSubmit = async () => {
    if (repair.fee) {
      try {
        const res = await fetch(
          `http://localhost:5197/api/Repair/${repair.id}`,
          {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(repair),
          }
        );
        if (res.status !== 200) {
          alert("Repair Update Failed!");
          return;
        }
        goto("inventory");
      } catch (error) {
        alert("Repair Update Failed!");
      }
    }
  };
</script>

<div class="container">
  {isFormInvalid}
  <h1 style="margin-bottom: 30px">Update Repair</h1>
  <form on:submit|preventDefault={handleSubmit}>
    <div class="mb-3">
      <label for="itemCode" class="form-label">Item Code</label>
      <input
        type="text"
        class="form-control form-control-sm"
        id="itemCode"
        readonly
        bind:value={repair.item.itemCode}
      />
    </div>
    <div class="mb-3">
      <label for="itemName" class="form-label">Item Name</label>
      <input
        type="text"
        class="form-control form-control-sm"
        id="itemName"
        bind:value={repair.item.itemName}
        readonly
      />
    </div>
    <div class="mb-3">
      <label for="contactNo" class="form-label">Contact No</label>
      <input
        type="text"
        class="form-control form-control-sm"
        id="contactNo"
        bind:value={repair.contactNo}
        readonly
      />
    </div>
    <div class="mb-3">
      <label for="issue" class="form-label">Issue</label>
      <input
        type="text"
        class="form-control form-control-sm"
        id="issue"
        bind:value={repair.issue}
        readonly
      />
    </div>
    <div class="mb-3">
      <label for="issue" class="form-label">Status</label>
      <select class="form-select form-select-sm" bind:value={repair.status}>
        <option value={0}>Open</option>
        <option value={1}>Fixed</option>
        <option value={2}>Delivered</option>
        <option value={3}>Unfixable</option>
      </select>
    </div>
    <div class="mb-3">
      <label for="issue" class="form-label">Issue</label>
      <input
        type="number"
        step=".01"
        class="form-control form-control-sm"
        id="issue"
        bind:value={repair.fee}
        required
      />
    </div>
    <button
      type="submit"
      class="btn btn-primary btn-sm"
      disabled={isFormInvalid}>Update</button
    >
  </form>
</div>

<style>
</style>
