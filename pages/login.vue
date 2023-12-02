<template>
    <div class="prose w-full max-w-2xl h-9">
        <h1>Log in to {{ title }}</h1>
        <button 
            class="mt-6 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
            @click="login">
            Log in with GitHub
        </button>
    </div>
</template>

<script lang='ts' setup>
    const { title } = useCourse();
    const login = () => {
        console.log('login');
    }
</script>