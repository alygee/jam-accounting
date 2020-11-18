<template>
  <div class="px-2">
    <img
      v-if="jar.volume === '1000'"
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
    <p v-if="jar.number">
      Number: <span class="font-bold">{{ jar.number }}</span>
    </p>
    <p>
      Volume: <span class="font-bold">{{ jar.volume }}</span>
    </p>
    <p v-if="jar.type">
      Jam: <span class="font-bold">{{ jar.type }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: "JarCard",
  props: ["jar"]
};
</script>
