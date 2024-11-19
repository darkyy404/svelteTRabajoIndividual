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
    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      z-index: 999;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  
    .modal {
      width: 90%;
      max-width: 400px;
      background: white;
      padding: 20px;
      border-radius: 16px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
      z-index: 1000;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }
  
    label {
      font-size: 0.9rem;
      color: #555;
    }
  
    input {
      width: 100%;
      padding: 10px;
      font-size: 1rem;
      border: 1px solid #ddd;
      border-radius: 8px;
      outline: none;
    }
  
    input:focus {
      border-color: #4a90e2;
    }
  
    button {
      flex: 1;
      padding: 10px;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
      cursor: pointer;
    }
  
    button:first-child {
      background: #4a90e2;
      color: white;
    }
  
    button:last-child {
      background: #f3f5f8;
      color: #555;
    }
  
    button:hover {
      opacity: 0.9;
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
  