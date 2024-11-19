<script>
    export let contacto;
    import { createEventDispatcher } from 'svelte';
  
    const dispatch = createEventDispatcher();
  
    const handleDelete = () => {
      dispatch('delete', contacto.id);
    };
  
    const handleEdit = () => {
      dispatch('edit', contacto);
    };
  </script>
  
  <style>
    .card {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 16px;
      background: white;
      border-radius: 12px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
      position: relative;
    }
  
    .card:hover {
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
  
    h3 {
      margin: 0;
      font-size: 1rem;
      color: #333;
    }
  
    p {
      margin: 0;
      font-size: 0.9rem;
      color: #a9b0c6;
    }
  
    button {
      background: transparent;
      border: none;
      font-size: 1.5rem;
      color: #a9b0c6;
      cursor: pointer;
    }
  
    button:hover {
      color: #4a90e2;
    }
  </style>
  
  <div class="card">
    <div>
      <h3>{contacto.nombre}</h3>
      <p>{contacto.email}</p>
    </div>
    <div>
      <span style="background: {contacto.online ? '#4caf50' : '#ccc'}; 
                    width: 10px; height: 10px; border-radius: 50%; display: inline-block;">
      </span>
      <button on:click={handleEdit} aria-label="Editar contacto">✏️</button>
      <button on:click={handleDelete} aria-label="Eliminar contacto">🗑️</button>
    </div>
  </div>
  