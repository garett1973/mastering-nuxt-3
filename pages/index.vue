<template>
  <div class="flex flex-col">
    <div class="mb-4">
      <h1>Home page</h1>
    </div>
    <NuxtLink class="underline font-medium" :to="firstLesson.path">
      Go to first lesson
    </NuxtLink>
  </div>
</template>

<script lang="ts" setup>
import useFirstLesson from "~/composables/useFirstLesson";
const firstLesson = useFirstLesson();
</script>
