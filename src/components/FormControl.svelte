<script>
  export let formStatus;

  const handleFormStatus = () => {
    formStatus = !formStatus;
  };
</script>

<header class="FormControl mb-4">
  <nav class="FormControl__nav">
    <button
      class:activeBtn={formStatus}
      on:click={handleFormStatus}
      class="FormControl__btn"
      type="button"
    >
      {#if formStatus}
        <i class="fa-solid fa-minus" />
      {:else}
        <i class="fa-solid fa-plus" />
      {/if}
    </button>
    <div class:hiddenForm={!formStatus} class=" FormControl__form card-body">
      <slot />
    </div>
  </nav>
</header>

<style>
  .FormControl__btn {
    margin: 0.5rem;
    position: fixed;
    top: 0.5rem;
    left: 0.5rem;
    text-align: center;
    width: 40px;
    height: 40px;
    font-weight: 500;
    border-radius: 50%;
    user-select: none;
    border: none;
    z-index: 150;
    color: #aaa;
    background: rgba(34, 34, 34, 0.3);
    box-shadow: 0 0 5px #212121;

    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
    transition: 0.23s;
  }

  .FormControl__btn:focus,
  .FormControl__btn:active {
    outline: none;
  }

  .FormControl__form {
    position: fixed;
    box-shadow: 0 0 5px #212121;
    z-index: 100;
    top: 1rem;
    left: 1rem;
    border-radius: 0.5rem;
    background: rgba(34, 34, 34, 0.3);
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
  }

  .hiddenForm {
    display: none;
  }

  .activeBtn {
    border-radius: 0.5rem 0 50% 0;
  }
</style>
