<template>
  <div id="app">
    <div class="container mx-auto mt-20 text-center text-gray-800">
      <h1 class="text-2xl font-bold my-10">
        Jam accounting system
      </h1>
      <div class="grid grid-cols-2 gap-4">
        <div class="bg-white rounded shadow-lg py-10">
          <button
            :class="{ 'font-bold': currentComponent === 'Jars' }"
            class="bg-purple-500 hover:bg-purple-700 text-white py-2 px-4 rounded mr-10"
            @click="currentComponent = 'Jars'"
          >
            Add jar
          </button>
          <button
            :class="{ 'font-bold': currentComponent === 'Jam' }"
            class="bg-purple-500 hover:bg-purple-700 text-white py-2 px-4 rounded"
            @click="currentComponent = 'Jam'"
          >
            Pour the jam
          </button>
          <keep-alive>
            <component
              v-bind:is="currentComponent"
              class="mt-10"
              :maxVolume="maxVolume"
              @add-jar="addJar"
              @pour-out="pourOut"
            />
          </keep-alive>
        </div>
        <div class="bg-white rounded shadow-lg p-10 text-center mb-10">
          <h2 class="font-bold text-2xl">State of the system</h2>
          <div v-if="emptyJars.length">
            <h3 class="font-bold text-lg mt-6 text-gray-700">Empty:</h3>
            <div class="flex items-center justify-center flex-wrap">
              <JarCard
                v-for="(jar, index) in emptyJars"
                :key="index"
                :jar="jar"
              />
            </div>
          </div>
          <div v-if="filledJars.length">
            <h3 class="font-bold text-lg mt-6 text-gray-700">Filled:</h3>
            <div class="flex items-center justify-center flex-wrap">
              <JarCard
                v-for="(jar, index) in filledJars"
                :key="index"
                :jar="jar"
              />
            </div>
          </div>
          <p v-if="!emptyJars.length && !filledJars.length" class="my-6">
            No jars!
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Jars from "./components/Jars.vue";
import Jam from "./components/Jam.vue";
import JarCard from "./components/JarCard.vue";

export default {
  name: "app",
  components: {
    Jars,
    Jam,
    JarCard
  },
  data: () => ({
    currentComponent: "Jars",
    emptyJars: [],
    filledJars: []
  }),
  computed: {
    maxVolume() {
      return this.emptyJars.reduce((sum, jar) => sum + Number(jar.volume), 0);
    }
  },
  methods: {
    addJar(jar) {
      this.emptyJars.push(jar);
    },
    pourOut(jam) {
      const emptyJars = [].concat(this.emptyJars);
      emptyJars.forEach(jar => {
        if (jam.qty <= 0) {
          return;
        }
        const el = this.emptyJars.find(j => j.number === jar.number);
        const idx = this.emptyJars.indexOf(el);
        this.emptyJars.splice(idx, 1);
        jar.type = jam.type;
        this.filledJars.push(jar);
        jam.qty -= Number(jar.volume);
      });
    }
  }
};
</script>
