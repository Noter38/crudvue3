<!-- src/components/FormComponent.vue -->
<template>
    <div>
      <form @submit.prevent="handleSubmit">
        <div>
          <label for="contrato">contratos asociados </label>
          <select id="contrato" v-model="form.contrato" required>
            <option disabled value="">Seleccione un contrato</option>
            <option>claro</option>
            <option>currupac</option>
            <option>uasl</option>
            <option>grupo k</option>
            <option>bluexpress</option>
          </select>
        </div>
        <div>
          <label for="total">total de licencias</label>
          <input type="text" id="total" v-model="form.total" required>
        </div>
        <div>
          <label for="estado">estado de la licencia </label>
          <select name="estado" v-model="form.estado" required>
            <option disabled value="">seleccione un estado </option>
            <option>activo</option>
            <option>inactivo</option>
          </select>
        </div>
        <div>
          <label for="fecha">fecha de inicio del contrato</label>
          <input type="date" id="fecha" v-model="form.fecha" required>
        </div>

        <button type="submit">{{ isEditing ? 'Actualizar' : 'Crear' }}</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      item: Object,
    },
    data() {
      return {
        form: {
          contrato: '',
         total: '',
          estado: '',
          fecha:'',
        },
        isEditing: false,
      };
    },
    watch: {
      item: {
        handler(newValue) {
          if (newValue) {
            this.form = { ...newValue };
            this.isEditing = true;
          } else {
            this.resetForm();
          }
        },
        deep: true,
        immediate: true,
      },
    },
    methods: {
      handleSubmit() {
        if (this.isEditing) {
          this.$emit('update-item', this.form);
        } else {
          this.$emit('add-item', this.form);
        }
        this.resetForm();
      },
      resetForm() {
        this.form = {
          contrato: '',
          total: '',
          estado: '',
          fecha: '',
        };
        this.isEditing = false;
      },
    },
  };
  </script>
  
  <style scoped>
  form {
    max-width: 400px;
    margin: 0 auto;
    padding: 1em;
    border: 1px solid #ccc;
    border-radius: 1em;
  }
  div {
    margin-bottom: 1em;
  }
  label {
    margin-bottom: .5em;
    color: #333333;
    display: block;
  }
  input, textarea, select {
    border: 1px solid #CCCCCC;
    padding: .5em;
    font-size: 1em;
    width: 100%;
    box-sizing: border-box;
    border-radius: 4px;
  }
  button {
    padding: 0.7em;
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
  