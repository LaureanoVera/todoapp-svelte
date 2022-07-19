<script>
  export let item;
  export let editItem;
  export let deleteItem;
</script>

<div class="rounded shadow mb-4">
  <div class="col">
    <div class="row">
      <div class="col-sm-4">
        <img
          src={item.imgUrl !== "" ? `${item.imgUrl}` : "images/image-empty.png"}
          alt={item.name}
          class="img-fluid"
        />
      </div>
      <div class="col-sm-8 ">
        <div class="card-body">
          <h5>{item.name}</h5>
          <span>
            <small>{item.cat}</small>
          </span>
          <p class="card-text">{item.desc}</p>
          <button
            on:click={() => editItem(item)}
            class="btn btn-light shadow-sm mr-2 rounded">Edit</button
          >
          <button
            on:click={() => deleteItem(item.id)}
            class="btn btn-danger shadow-sm rounded">Delete</button
          >
        </div>
      </div>
    </div>
  </div>
</div>
