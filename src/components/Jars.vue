<template>
  <div>
    <AddJarForm @add-jar="$emit('add-jar', $event)" />
  </div>
</template>

<script>
import AddJarForm from "./AddJarForm.vue";

export default {
  name: "Jars",
  components: { AddJarForm }
};
</script>
