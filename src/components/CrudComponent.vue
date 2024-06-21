<!-- src/components/CrudComponent.vue -->
<template>
    <div>
      <h2>Mantenedor de Elementos</h2>
      <FormComponent @add-item="addItem" @update-item="updateItem" :item="currentItem"/>
      <table>
        <thead>
          <tr>
            <th>contrato</th>
            <th>total</th>
            <th>estado</th>
            <th>fecha</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in items" :key="item.id">
            <td>{{ item.contrato}}</td>
            <td>{{ item.total}}</td>
            <td>{{ item.estado}}</td>
            <td>{{ item.fecha}}</td>
            <td>
              <button @click="editItem(item)">Editar</button>
              <button @click="deleteItem(item.id)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import FormComponent from './FormComponent.vue';
  
  export default {
    components: {
      FormComponent,
    },
    data() {
      return {
        items: [],
        currentItem: null,
      };
    },
    methods: {
      addItem(item) {
        item.id = Date.now();
        this.items.push(item);
      },
      updateItem(updatedItem) {
        const index = this.items.findIndex(item => item.id === updatedItem.id);
        if (index !== -1) {
          this.$set(this.items, index, updatedItem);
        }
      },
      editItem(item) {
        this.currentItem = { ...item };
      },
      deleteItem(id) {
        this.items = this.items.filter(item => item.id !== id);
      },
    },
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    padding: 8px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }
  button {
    padding: 0.5em;
    color: #fff;
    background-color: #007BFF;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  button:hover {
    background-color: #0056b3;
  }
  </style>
  