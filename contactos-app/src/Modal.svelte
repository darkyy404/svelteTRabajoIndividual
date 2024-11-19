<script>
    export let isOpen = false;
    export let title = '';
    export let contact = { nombre: '', email: '' };
    export let onSubmit;
  
    const handleSubmit = () => {
      onSubmit(contact);
      isOpen = false;
    };
  </script>
  
  <style>
    .modal {
      display: flex;
      flex-direction: column;
      gap: 12px;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
      z-index: 1000;
      width: 90%;
      max-width: 400px;
    }
    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.5);
      z-index: 999;
    }
  </style>
  
  {#if isOpen}
    <div class="overlay" on:click={() => (isOpen = false)}></div>
    <div class="modal">
      <h2>{title}</h2>
      <label>
        Nombre:
        <input type="text" bind:value={contact.nombre} placeholder="Introduce el nombre" />
      </label>
      <label>
        Email:
        <input type="email" bind:value={contact.email} placeholder="Introduce el email" />
      </label>
      <div>
        <button on:click={handleSubmit}>Guardar</button>
        <button on:click={() => (isOpen = false)}>Cancelar</button>
      </div>
    </div>
  {/if}
  