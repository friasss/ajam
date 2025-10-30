<script setup>
import { ref } from 'vue'

const nombre = ref('')
const correo = ref('')
const contrasena = ref('')

const registrarUsuario = async () => {
  const datosUsuario = {
    nombre: nombre.value,
    correo: correo.value,
    contrasena: contrasena.value
  }

  try {
    const respuesta = await fetch('https://backend-2-e81r.onrender.com/registrar', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(datosUsuario)
    });

    const data = await respuesta.json();

    if (!respuesta.ok) {
      throw new Error(data.mensaje || data.error || 'Error al procesar la solicitud');
    }

    alert(data.mensaje); 
    
    nombre.value = ''
    correo.value = ''
    contrasena.value = ''

  } catch (error) {
    console.error('Error al registrar usuario:', error);
    alert(`Error: ${error.message}`);
  }
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
  /* Más grande y con fondo blanco limpio */
  max-width: 450px; /* Más ancho */
  width: 100%;
  margin: 2rem auto;
  padding: 2.5rem; /* Más espaciado interno */
  border: none;
  border-radius: 12px; /* Bordes más redondeados */
  background-color: #ffffff; /* Blanco puro */
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1); /* Sombra suave */
}

h2 {
  text-align: center;
  margin-bottom: 2rem;
  color: #333; /* Color oscuro para el título */
  font-size: 1.75rem; /* Título más grande */
  font-weight: 600;
}

.form-group {
  margin-bottom: 1.5rem; /* Más espacio entre campos */
}

.form-group label {
  display: block;
  margin-bottom: 0.6rem;
  font-weight: 600;
  color: #555; /* ¡EL ARREGLO! Color oscuro para las etiquetas */
  font-size: 0.9rem;
}

.form-group input {
  width: 100%;
  padding: 0.85rem; /* Inputs más altos */
  box-sizing: border-box;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 1rem; /* Texto de input más grande */
  color: #333; /* Color del texto que escribes */
  background-color: #f9f9f9; /* Fondo ligero para el input */
  transition: all 0.2s ease;
}

/* Efecto al hacer clic en un input */
.form-group input:focus {
  outline: none;
  border-color: #42b983;
  box-shadow: 0 0 0 3px rgba(66, 185, 131, 0.2);
  background-color: #fff;
}

button {
  width: 100%;
  padding: 0.9rem; /* Botón más grande */
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1.1rem; /* Texto de botón más grande */
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

button:hover {
  background-color: #349a6c;
}

button:active {
  transform: scale(0.98); /* Pequeño efecto al hacer clic */
}
</style>