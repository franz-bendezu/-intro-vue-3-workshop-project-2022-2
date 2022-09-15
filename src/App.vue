<script>
import CounterButton from "./components/CounterButton.vue";

export default {
  components: {
    CounterButton,
  },
  data() {
    return {
      title: "Mis Actividades",
      containerId: "container",
      blockId: "block",
      isButtonDisabled: true,
      date: "2022-31-08",
      today: "2022-21-08",
      done: true,
      items: ["Pera", "Manzana", "Platano", "Naranja", "Durazno"],
      object: {
        propiedad1: "Valor 1",
        propiedad2: "Valor 2",
        propiedad3: "Valor 3",
      },
      count: 0,
      email: "example@gmail.com",
      tab: "tab-10",
      fullName: "",
      fullNameError: false,
      username: "",
      isSearchingUsername: false,
    };
  },
  methods: {
    incrementCount($event) {
      console.log($event);
      this.count++;
    },
    updateEmail($event) {
      console.log($event);
      console.log($event.target.value);
      this.email = $event.target.value;
    },
    validateFullName() {
      if (this.fullName.length > 10) {
        this.fullNameError = true;
      } else {
        this.fullNameError = false;
      }
    },
    getDoubleCount() {
      console.log("getDoubleCount");
      return this.count * 2;
    },
    print(value) {
      console.log(value);
    },
  },
  computed: {
    doubleCount() {
      console.log("doubleCount");
      return this.count * 2;
    },
  },
  watch: {
    doubleCount(newValue, oldValue) {
      this.print(newValue);
      this.print(oldValue);
    },
    username(newValue) {
      this.print(newValue);
      this.isSearchingUsername = true;
      setTimeout(() => {
        this.isSearchingUsername = false;
      }, 2000);
    },
  },
};
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />
  </header>
  <main class="container">
    <!---// mustache (textos en la plantilla) -->
    {{ tab }}
    <select v-model="tab">
      <option value="tab-1">Enlace a propiedades</option>
      <option value="tab-2">Renderizado condicional</option>
      <option value="tab-3">Renderizado de listas</option>
      <option value="tab-4">Manejo de eventos</option>
      <option value="tab-5">Enlace bidireccional</option>
      <option value="tab-6">Enlace de Estilo</option>
      <option value="tab-7">Enlace de clases</option>
      <option value="tab-8">Propiedades computadas</option>
      <option value="tab-9">Observadores</option>
      <option value="tab-10">Componentes</option>
    </select>
    <div>{{ title }}</div>
    <!---// Enlace a propiedades -->
    <div v-if="tab === 'tab-1'">
      <div v-bind:id="containerId"></div>
      <div :id="blockId"></div>
      <button :disabled="isButtonDisabled">Click me!</button>
    </div>
    <!---// Renderizado condicional -->
    <div v-else-if="tab === 'tab-2'">
      <div v-if="today == date">Is Today!</div>
      <div v-else-if="done">Is Done!</div>
      <span v-else>Not is Today :c</span>
      <div v-show="today == date">Is Today!</div>
    </div>
    <!---// Renderizado de listas -->
    <div v-else-if="tab === 'tab-3'">
      Mis frutas preferidas:
      <ul>
        <li v-for="item in items" :key="item">
          {{ item }}
        </li>
      </ul>
      <ul>
        <li v-for="(item, index) in items" :key="item">
          {{ item }} : {{ index }}
        </li>
      </ul>
      <ul>
        <li v-for="(item, index) of items" :key="index">
          {{ item }} : {{ index }}
        </li>
      </ul>
      <ul>
        <li v-for="(value, key) of object" :key="key">
          {{ key }} : {{ value }}
        </li>
      </ul>
    </div>
    <!---// Manejo de eventos-->
    <div v-else-if="tab === 'tab-4'">
      <div>{{ count }}</div>
      <button v-on:click="count = count + 1">Increase</button>
      <button @click="incrementCount">Increase</button>
      <button @click="incrementCount()">Increase</button>
    </div>
    <!---// Enlace bidireccional -->
    <div v-else-if="tab === 'tab-5'">
      <div>{{ email }}</div>
      v-model: <input v-model="email" />
      <br />
      v-model.trim <input v-model.trim="email" />
      <br />
      change event <input :value="email" @change="updateEmail" />
      <br />
      update event <input :value="email" @input="updateEmail" />
      <br />
      v-model.lazy <input v-model.lazy="email" />
    </div>
    <div v-else-if="tab === 'tab-6'">
      <input v-model="fullName" />
      <div :style="{ color: fullNameError ? '#bb2124' : '#22bb33' }">
        {{ fullNameError ? "Campo incorrecto" : "Campo correcto" }}
      </div>
      {{ fullNameError }}
      <button @click="validateFullName">Enviar</button>
    </div>
    <div v-else-if="tab === 'tab-7'">
      <div class="field">
        <label class="label">Nombres completos</label>
        <div class="control">
          <input
            v-model="fullName"
            class="input"
            :class="{
              'is-danger': fullNameError,
              'is-success': !fullNameError,
            }"
            type="email"
            placeholder="Email input"
          />
        </div>
        <p class="help" :class="[fullNameError ? 'is-danger' : 'is-success']">
          {{ fullNameError ? "Campo incorrecto" : "Campo correcto" }}
        </p>
      </div>
      <div class="field is-grouped">
        <div class="control">
          <button @click="validateFullName" class="button is-link">
            Validar
          </button>
        </div>
      </div>
    </div>
    <div v-else-if="tab === 'tab-8'">
      <p class="title is-4">Contador: {{ count }}</p>
      <p class="title is-4">Contador x2: {{ doubleCount }}</p>
      <p class="title is-4">Contador x2: {{ getDoubleCount() }}</p>
      <div class="field is-grouped">
        <div class="control">
          <button @click="incrementCount" class="button is-link">
            Aumentar
          </button>
        </div>
      </div>
    </div>

    <div v-else-if="tab === 'tab-9'">
      <div class="field">
        <label class="label">Nombres de usuario</label>
        <div class="control">
          <input
            v-model.lazy="username"
            class="input"
            type="text"
            placeholder="Ingrese nombre de usuario"
          />
        </div>
      </div>
      <p v-if="isSearchingUsername" class="help">Buscando...</p>
    </div>
    <div v-else-if="tab === 'tab-10'">
      <counter-button></counter-button>
      <CounterButton color="info"></CounterButton>
      <counter-button :color="undefined"></counter-button>
      <counter-button :color="null"></counter-button>
      <counter-button :color="2"></counter-button>
      <CounterButton color="info"><div>Probando slot</div> </CounterButton>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
