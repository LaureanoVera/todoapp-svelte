<script>
  import Form from "./components/Form.svelte";
  import FormControl from "./components/FormControl.svelte";
  import Card from "./components/Card.svelte";
  import Author from "./components/Author.svelte";

  let items = [];
  let item = {};
  let editStatus = false;
  let formStatus = false;

  const loadItems = () => {
    items = JSON.parse(localStorage.getItem("items")) || [];
  };

  const cleanItem = () => {
    item = {
      id: "",
      name: "",
      desc: "",
      date: "2022-12-17",
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
    formStatus = true;
  };

  const deleteItem = (id) => {
    items = items.filter((item) => item.id !== String(id));
    localStorage.setItem("items", JSON.stringify(items));
  };

  const updateItem = () => {
    let update = { ...item };
    const index = items.findIndex((item) => item.id === update.id);
    if (update.cat === "") {
      update.cat = "Others";
    }
    items[index] = update;
    localStorage.setItem("items", JSON.stringify(items));
    cleanItem();
    editStatus = false;
    formStatus = false;
  };

  const addItem = () => {
    const idCode = new Date().getTime();
    if (item.cat === "") {
      item.cat = "Others";
    }
    item.id = `${idCode}-${item.cat}`;
    items.push(item);
    localStorage.setItem("items", JSON.stringify(items));
    cleanItem();
    formStatus = false;
    loadItems();
  };

  const handleSubmit = () => {
    if (!editStatus) {
      addItem();
    } else {
      updateItem();
    }
  };

  cleanItem();
  loadItems();
</script>

<FormControl {formStatus}>
  <Form on:submit={handleSubmit} {item} {editStatus} />
</FormControl>
<main>
  <Author />
  <section class="container pt-4">
    <article class="row">
      {#each items as item, i}
        <Card {editItem} {deleteItem} {item} />
      {/each}
    </article>
  </section>
</main>

<style>
  :global(:root) {
    --main-red: #d9534f;
  }

  :global(*) {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: "Montserrat", sans-serif;
  }
</style>
