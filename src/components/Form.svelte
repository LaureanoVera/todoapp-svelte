<script>
  export let item;
  export let editStatus;
</script>

<form on:submit|preventDefault>
  <div class="form-group">
    <input
      bind:value={item.name}
      required
      type="text"
      placeholder="Name"
      id="itemName"
      class="form-control rounded-top my-2"
    />
  </div>
  <div class="form-group">
    <textarea
      bind:value={item.desc}
      required
      id="itemDescription"
      rows="3"
      placeholder="Description"
      class="form-control my-2"
    />
  </div>
  <div class="form-group">
    <input
      bind:value={item.date}
      required
      type="date"
      id="itemDateTime"
      class="form-control my-2"
    />
  </div>
  <div class="form-group">
    <input
      bind:value={item.imgUrl}
      type="url"
      id="itemImageUrl"
      placeholder="https://imageurl.here"
      class="form-control my-2"
    />
  </div>
  <div class="form-group">
    <input
      bind:value={item.cat}
      type="text"
      placeholder="Category"
      id="itemCat"
      class="form-control my-2"
    />
  </div>
  <input
    type="submit"
    value={editStatus ? "Update" : "Save"}
    class="btn btn-dark col-12 rounded-bottom my-2"
  />
</form>
