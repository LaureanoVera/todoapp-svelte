<script>
  import Form from "./components/Form.svelte";
  import Card from "./components/Card.svelte";
  import Noty from "noty";

  let items = [
    {
      id: "25251525",
      name: "Name",
      desc: "Bla blalbblab lab lala",
      cat: "",
      imgUrl: "images/image-empty.png",
    },
  ];

  let item = {};

  let editStatus = false;

  const cleanItem = () => {
    item = {
      id: "",
      name: "",
      desc: "",
      cat: "",
      imgUrl: "",
    };
  };

  const editItem = (edit) => {
    if (edit.imgUrl === "images/image-empty.png") {
      edit.imgUrl = "";
    }
    item = edit;
    editStatus = true;
  };

  const deleteItem = (id) => {
    items = items.filter((item) => item.id !== id);
  };

  const updateItem = () => {
    let update = { ...item };
    const index = items.findIndex((item) => item.id === update.id);
    if (update.cat === "") {
      update.cat = "Others";
    }
    items[index] = update;
    cleanItem();
    editStatus = false;
    new Noty({
      theme: "sunset",
      type: "alert",
      timeout: 2000,
      text: "Update Successfully",
    }).show();
  };

  const addItem = () => {
    const idCode = new Date().getTime();
    if (item.cat === "") {
      item.cat = "Others";
    }
    item.id = `${idCode}-${item.cat}`;
    items = items.concat(item);
    cleanItem();
  };

  const handleSubmit = () => {
    if (!editStatus) {
      addItem();
    } else {
      updateItem();
    }
  };

  cleanItem();

  // LocalStorage
  if (typeof Storage !== "undefined") {
    // LocalStorage disponible
    localStorage.setItem("itemsList", JSON.stringify(items));
  } else {
    // LocalStorage no soportado en este navegador
  }
  let itemsList = JSON.parse(localStorage.getItem("itemsList"));
  console.log(itemsList);
</script>

<main>
  <section class="container">
    <article class="row">
      {#each items as item, i}
        <Card {editItem} {deleteItem} {item} />
      {/each}
    </article>
    <article class="row">
      <div class="col-12">
        <div class="card-body shadow rounded">
          <Form on:submit={handleSubmit} {item} {editStatus} />
        </div>
      </div>
    </article>
  </section>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
