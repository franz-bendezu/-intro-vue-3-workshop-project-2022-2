<script>
export default {
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
    };
  },
  methods: {
    incrementCount($event) {
      console.log($event);
      this.count++;
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
  <main>
    <!---// mustache (textos en la plantilla) -->
    <div>{{ title }}</div>
    <!---// Enlace a propiedades -->
    <div>
      <div v-bind:id="containerId"></div>
      <div :id="blockId"></div>
      <button :disabled="isButtonDisabled">Click me!</button>
    </div>
    <!---// Renderizado condicional -->
    <div>
      <div v-if="today == date">Is Today!</div>
      <div v-else-if="done">Is Done!</div>
      <span v-else>Not is Today :c</span>
      <div v-show="today == date">Is Today!</div>
    </div>
    <!---// Renderizado de listas -->
    <div>
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
    <div>
      <div>{{ count }}</div>
      <button v-on:click="count = count + 1">Increase</button>
      <button @click="incrementCount">Increase</button>
      <button @click="incrementCount()">Increase</button>
    </div>
    <!---// Enlace bidireccional -->
    <div>
      <div>{{ email }}</div>
      <input v-model="email" />
      <input v-model.trim="email" />
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
