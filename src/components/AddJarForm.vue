<template>
  <form class="w-2/3 text-center mx-auto">
    <img
      v-if="volume === '1000'"
      src="../assets/images/big.png"
      alt="empty jar image"
      class="w-20 mx-auto"
    />
    <img
      v-else
      src="../assets/images/small.png"
      alt="empty jar image"
      class="w-20 mx-auto"
    />
    <input
      class="shadow border rounded w-full py-2 px-3 text-gray-700 my-4"
      v-model="number"
      type="text"
      placeholder="Number of jar"
    />
    <select
      class="bg-white w-full border text-gray-700 py-3 px-4 rounded shadow"
      v-model="volume"
    >
      <option value="500">500 ml</option>
      <option value="1000">1 l</option>
    </select>
    <button
      :class="[isDisabled ? disabled : '']"
      class="bg-purple-500 hover:bg-purple-700 text-white py-2 px-4 rounded mt-4 font-bold"
      @click="add"
      type="button"
    >
      Add
    </button>
  </form>
</template>

<script>
export default {
  name: "AddJarForm",
  data: () => ({
    number: "",
    volume: 500,
    disabled: "opacity-50 cursor-not-allowed"
  }),
  computed: {
    isDisabled() {
      return !this.number;
    }
  },
  methods: {
    add() {
      if (this.number) {
        this.$emit("add-jar", {
          number: this.number,
          volume: this.volume
        });
      }
    }
  }
};
</script>
