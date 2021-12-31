<template>
  <div>
    <v-chip
      class="mx-1 my-2"
      color="primary"
      text-color="white"
      v-for="classmate in classmates"
      :key="classmate"
      v-ripple
    >
      <v-avatar left color="accent">{{ classmate.substring(0,1) }}</v-avatar>
      {{ classmate }}
    </v-chip>
  </div>
</template>

<script>
export default {
  props: {
    classmates: {
      required: true,
    },
  },
};
</script>

<style scoped>
</style>