<script>
  export let item;
  export let editItem;
  export let deleteItem;
</script>

<div class="Card p-2 col-md-8 offset-md-2 shadow mb-4">
  <div class="row">
    <div class="col">
      <img
        src={item.imgUrl !== "" ? `${item.imgUrl}` : "images/image-empty.png"}
        alt={item.name}
        class="Card__img img-fluid"
      />
    </div>
    <div class="Card__body col-sm">
      <div class="card-body">
        <h5 class="Card__name">{item.name}</h5>
        <span>
          <small>{item.cat}</small>
        </span>
        <br />
        <span>
          <small class="Card__span">Complete Before: {item.date}</small>
        </span>
        <p class="Card__desc card-text">{item.desc}</p>
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

<style>
  .Card {
    background: rgba(34, 34, 34, 0.3);
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
    color: #eee;
    border-radius: 0.5rem;
    user-select: none;
  }

  .Card__img {
    width: 100%;
    max-width: 220px;
    height: 220px;
    object-fit: cover;
  }

  .Card__span {
    font-weight: 600;
  }

  @media (max-width: 576px) {
    .Card {
      margin: 0 0.75rem;
      text-align: center;
    }

    .Card__img {
      width: 100%;
      max-width: 220px;
      max-height: 220px;
    }
  }
</style>
