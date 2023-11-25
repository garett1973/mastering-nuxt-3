<template>
  <NuxtLayout>
    <div class="prose">
      <h1>Dang</h1>
            <p>
              <strong>{{ error.message }}</strong>
            </p>
      <p>It looks like something broke.</p>
      <p>Sorry about that.</p>
      <p>
        <button 
          class="bg-gray-300 rounded pb-3 pt-2 px-6 mt-4 hover:bg-gray-600 hover:cursor-pointer hover:text-white transition-colors duration-200 ease-in-out" 
          @click="handleError(error)">
            Try again
        </button>
      </p>
    </div>
  </NuxtLayout>
</template>

<script setup>
const error = useError();

const handleError = () => {
  clearError({
    redirect: '/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vuejs-3',
  });
};

</script>