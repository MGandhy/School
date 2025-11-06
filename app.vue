<script setup>
import { ref } from "vue";

const role = ref(null);
const students = ref([
  { nombre: "María Pérez", correo: "maria@example.com", grado: "8°" }
]);
const teachers = ref([
  { nombre: "Juan Gómez", correo: "juan@example.com", asignatura: "Matemáticas" }
]);

const form = ref({ nombre: "", correo: "", direccion: "", grado: "", asignatura: "" });

function register() {
  if (role.value === "student") students.value.push({ ...form.value });
  else if (role.value === "teacher") teachers.value.push({ ...form.value });
  form.value = { nombre: "", correo: "", direccion: "", grado: "", asignatura: "" };
}
</script>

<template>
  <div>
    <header>
      <h1>I.E. Montería Paz</h1>
      <p>Montería, Córdoba — Colombia</p>
    </header>

    <div class="card">
      <h2>Bienvenidos</h2>
      <p><b>Misión:</b> Formar ciudadanos íntegros con valores y conocimiento tecnológico.</p>
      <p><b>Visión:</b> Ser una institución líder en educación innovadora en Montería.</p>
      <p><b>Historia:</b> Fundada en 1995, ha promovido la paz y la inclusión educativa.</p>
    </div>

    <div class="card">
      <h3>Ingresar como:</h3>
      <button @click="role = 'student'">Estudiante</button>
      <button @click="role = 'teacher'">Docente</button>
    </div>

    <div v-if="role" class="card">
      <h3>Matrícula ({{ role === 'student' ? 'Estudiante' : 'Docente' }})</h3>
      <form @submit.prevent="register">
        <label>Nombre:</label>
        <input v-model="form.nombre" required />
        <label>Correo:</label>
        <input v-model="form.correo" type="email" required />
        <label>Dirección:</label>
        <input v-model="form.direccion" required />
        <label v-if="role==='student'">Grado:</label>
        <input v-if="role==='student'" v-model="form.grado" placeholder="Ej: 8°" />
        <label v-if="role==='teacher'">Asignatura:</label>
        <input v-if="role==='teacher'" v-model="form.asignatura" placeholder="Ej: Matemáticas" />
        <button type="submit">Registrar</button>
      </form>
    </div>

    <div v-if="role==='student'" class="card">
      <h3>Estudiantes Registrados</h3>
      <table>
        <tr><th>Nombre</th><th>Correo</th><th>Grado</th></tr>
        <tr v-for="s in students" :key="s.correo">
          <td>{{ s.nombre }}</td><td>{{ s.correo }}</td><td>{{ s.grado }}</td>
        </tr>
      </table>
    </div>

    <div v-if="role==='teacher'" class="card">
      <h3>Docentes Registrados</h3>
      <table>
        <tr><th>Nombre</th><th>Correo</th><th>Asignatura</th></tr>
        <tr v-for="t in teachers" :key="t.correo">
          <td>{{ t.nombre }}</td><td>{{ t.correo }}</td><td>{{ t.asignatura }}</td>
        </tr>
      </table>
    </div>

    <footer>
      © 2025 I.E. Montería Paz — contacto@iemonteriapaz.edu.co
    </footer>
  </div>
</template>

