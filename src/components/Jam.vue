<template>
  <form class="w-2/3 mx-auto">
    <p>
      Maximum possible volume is
      <span class="font-bold text-lg">{{ maxVolume }} ml</span>
    </p>
    <input
      class="shadow border rounded w-full py-2 px-3 text-gray-700 my-4"
      v-model="qty"
      :max="maxVolume"
      type="number"
      placeholder="Amount of jam (in ml)"
    />
    <select
      class="bg-white w-full border text-gray-700 py-3 px-4 rounded shadow"
      v-model="type"
    >
      <option value="strawberry">Strawberry</option>
      <option value="cherry">Cherry</option>
      <option value="apricot">Apricot</option>
    </select>
    <button
      :class="[isDisabled ? disabled : '']"
      class="bg-purple-500 hover:bg-purple-700 text-white py-2 px-4 rounded mt-4 font-bold"
      @click="$emit('pour-out', { qty, type })"
      type="button"
    >
      Pour out
    </button>
  </form>
</template>

<script>
export default {
  name: "Jam",
  props: ["maxVolume"],
  data: () => ({
    qty: 0,
    type: "strawberry",
    disabled: "opacity-50 cursor-not-allowed"
  }),
  computed: {
    isDisabled() {
      return !this.qty || this.qty > this.maxVolume;
    }
  }
};
</script>
