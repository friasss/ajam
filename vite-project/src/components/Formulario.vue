<script setup>
import { ref } from 'vue'

const nombre = ref('')
const correo = ref('')
const contrasena = ref('')

const registrarUsuario = () => {
  const datosUsuario = {
    nombre: nombre.value,
    correo: correo.value,
    contrasena: contrasena.value
  }

  console.log('Enviando al backend:', datosUsuario)

  nombre.value = ''
  correo.value = ''
  contrasena.value = ''
}
</script>

<template>
  <div class="formulario-container">
    <h2>Registro de Usuario</h2>
    
    <form @submit.prevent="registrarUsuario">
      
      <div class="form-group">
        <label for="nombre">Nombre:</label>
        <input 
          type="text" 
          id="nombre" 
          v-model="nombre" 
          required 
        />
      </div>

      <div class="form-group">
        <label for="correo">Correo Electrónico:</label>
        <input 
          type="email" 
          id="correo" 
          v-model="correo" 
          required 
        />
      </div>

      <div class="form-group">
        <label for="contrasena">Contraseña:</label>
        <input 
          type="password" 
          id="contrasena" 
          v-model="contrasena" 
          required 
          minlength="6" 
        />
      </div>

      <button type="submit">Registrar</button>
    </form>
  </div>
</template>

<style scoped>
.formulario-container {
  max-width: 400px;
  margin: 2rem auto;
  padding: 1.5rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
}

h2 {
  text-align: center;
  margin-bottom: 1.5rem;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

.form-group input {
  width: 100%;
  padding: 0.5rem;
  box-sizing: border-box;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  width: 100%;
  padding: 0.75rem;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
}

button:hover {
  background-color: #349a6c;
}
</style>