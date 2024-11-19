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
      padding: 12px;
      background: #f5f5f5;
      border-radius: 8px;
      position: relative;
    }
  </style>
  
  <div class="card">
    <div>
      <h3>{contacto.nombre}</h3>
      <p>{contacto.email}</p>
    </div>
    <div>
      <span>{contacto.online ? '🟢' : '⚪'}</span>
      <button on:click={handleEdit}>✏️</button>
      <button on:click={handleDelete}>🗑️</button>
    </div>
  </div>
  