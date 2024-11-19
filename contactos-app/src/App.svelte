<script>
	import { onMount } from 'svelte';
	import ContactCard from './ContactCard.svelte';
	import Modal from './Modal.svelte';
  
	let searchQuery = '';
	let contactos = [
	  { id: 1, nombre: 'Vincent Moody', email: 'vincent.moody@gmail.com', online: true },
	  { id: 2, nombre: 'Bradley Malone', email: 'bradley.m@gmail.com', online: true },
	  { id: 3, nombre: 'Janie Todd', email: 'stroman.hanna@yahoo.com', online: false },
	  { id: 4, nombre: 'Marvin Lambert', email: 'micalea.okuneva@zemlak.biz', online: true },
	  { id: 5, nombre: 'Teresa Lloyd', email: 'carlee_erdman@gmail.com', online: true },
	  { id: 6, nombre: 'Fred Haynes', email: 'jarod.miller@hotmail.com', online: false },
	  { id: 7, nombre: 'Rose Peters', email: 'oma.russel@hotmail.com', online: true },
	];
  
	let filteredContacts = contactos;
	let showModal = false;
	let modalTitle = '';
	let modalContact = { id: null, nombre: '', email: '' };
	let editingContact = false;
  
	// Filtrar contactos con base en la búsqueda
	const filterContacts = () => {
	  filteredContacts = contactos.filter(contacto =>
		contacto.nombre.toLowerCase().includes(searchQuery.toLowerCase()) ||
		contacto.email.toLowerCase().includes(searchQuery.toLowerCase())
	  );
	};
  
	// Abrir el modal (para crear o editar)
	const openModal = (contact = null) => {
	  modalTitle = contact ? 'Editar Contacto' : 'Crear Contacto';
	  modalContact = contact
		? { ...contact }
		: { id: null, nombre: '', email: '' };
	  editingContact = !!contact;
	  showModal = true;
	};
  
	// Manejar el envío del modal
	const handleModalSubmit = (contact) => {
	  if (editingContact) {
		// Actualizar contacto existente
		contactos = contactos.map(c =>
		  c.id === contact.id ? { ...c, ...contact } : c
		);
	  } else {
		// Crear un nuevo contacto
		contactos = [...contactos, { id: Date.now(), ...contact }];
	  }
	  filterContacts();
	  showModal = false;
	};
  
	// Eliminar un contacto
	const deleteContact = (id) => {
	  contactos = contactos.filter(contacto => contacto.id !== id);
	  filterContacts();
	};
  
	onMount(() => {
	  filterContacts();
	});
  </script>
  
  <style>
	.container {
	  padding: 20px;
	  max-width: 600px;
	  margin: auto;
	}
	.header {
	  display: flex;
	  justify-content: space-between;
	  align-items: center;
	}
	.search-bar {
	  display: flex;
	  gap: 8px;
	  margin: 16px 0;
	}
	.list {
	  display: flex;
	  flex-direction: column;
	  gap: 12px;
	}
  </style>
  
  <div class="container">
	<div class="header">
	  <h1>Contactos</h1>
	  <button on:click={() => openModal()}>➕</button>
	</div>
	<div class="search-bar">
	  <input
		type="text"
		bind:value={searchQuery}
		placeholder="Buscar..."
		on:input={filterContacts}
	  />
	  <button>🔍</button>
	</div>
	<div class="list">
	  {#each filteredContacts as contacto}
		<ContactCard
		  {contacto}
		  on:edit={(e) => openModal(e.detail)}
		  on:delete={(e) => deleteContact(e.detail)}
		/>
	  {/each}
	</div>
  
	<Modal
	  bind:isOpen={showModal}
	  title={modalTitle}
	  bind:contact={modalContact}
	  onSubmit={handleModalSubmit}
	/>
  </div>
  