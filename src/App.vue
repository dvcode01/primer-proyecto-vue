<!-- Las variables se escriben en el html con doble llaves -->
<!-- V-bind permite enlazar valores a los atributos HTML -->
<!-- Las expresiones son posibles utilizarlas incluso las ternarias -->
<!-- Las directivas son atributos especiales (v-) y realizan actualizaciones reactivas -->
<!-- V-if y V-else funcionan similar al if y el else tradicionales, pero el segundo debe ir seguido del primero -->
<!-- V-show muestra o oculta un elemento, lo hace cambiando el display en el CSS -->
<!-- En términos generales, v-if tiene costos de alternancia más altos mientras que v-show tiene costos de renderización inicial más altos. Así que prefiera v-show si necesita alternar algo con mucha frecuencia, y prefiera v-if si es poco probable que la condición cambie en el tiempo de ejecución. -->
<!-- V-for se usa para iterar  y para rastrear la identidad de cada nodo, debemos usar una key unica para cada elemento. En el caso de los objetos, el segundo parametro no hara referencia al indice, sino de la propiedad y el ultimo si seria el indice -->
<!-- El V-if siempre tendra mayor prioridad que el V-for, lo que implica que el primero no tendra acceso a los valores/variables del segundo -->
<!-- V-on se usa para escuchar los eventos del DOM, puedes escribirlo tambien con un arroba (@) -->
<!-- ref() es una forma de trabajar con reactividad en vue 3, Es una referencia reactiva que toma el argumento y lo devuelve envuelto dentro de un objeto con una value propiedad, que luego puede usarse para acceder o mutar el valor de la variable reactiva.-->
<!-- Las propiedades computadas nos sirven para generar calculos en nuestros componentes, por ejemplo no se recomienda colocar demasiada lógica en nuestras plantillas HTML, ya que dificulta la interpretación de nuestros componentes. -->


<script setup>
  import { ref, computed } from 'vue';
  const name = 'Vue 3';
  let counter = ref(0);
  let favoriteNumbers = ref([]);

  const classCounter = computed(() => {
    if(counter.value === 0){
      return 'zero';
    }

    if(counter.value > 0){
      return 'positive';
    }
    
    if(counter.value < 0){
      return 'negative';
    }
  });
  
  // metodo - methods
  const increment = () => counter.value++;

  const reset = () => counter.value = 0;
  
  const decrement = () => counter.value--;

  const addNumber = () => {
    favoriteNumbers.value.push(counter.value);
  }

  const blockButton = computed(() => {
    const numberSearch = favoriteNumbers.value.find(value => value === counter.value);

    return numberSearch || numberSearch === 0;
  })
</script>

<template>
  <div class="container text-center">
    <h1>Hola mundo {{name}}!</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-warning text-white">Resetear</button>
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="addNumber" :disabled="blockButton" class="btn btn-primary">Agregar</button>
    </div>
    <ul class="list-group mt-3">
      <li v-for="(value, index) in favoriteNumbers" :key="index" class="list-group-item">
        {{ value }}
      </li>
    </ul>
  </div>
</template>

<style>
h1{
  color: orange;
}
.positive{
  color: green;
}
.negative{
  color: red;
}
.zero{
  color: peru;
}
</style>