<template>
    <div class="flex flex-col h-screen">
        <div>
            <div class="flex justify-center w-full bg-gray-100 my-6">
                <h1 class="text-3xl font-bold">
                    Course: Mastering Nuxt 3
                </h1>
            </div>
        </div>
        <div class="flex flex-grow">
            <div class="flex flex-row w-full">
                <div class="w-1/4 ml-6 mr-4 mt-4 bg-white rounded-md p-5 my-6">
                    <p class="text-xl font-bold mb-6">Chapters</p>
                    <div
                        class="space-y-1 mb-4 flex flex-col"
                        v-for="chapter in chapters"
                        :key="chapter.slug"
                        >
                        <h4 class="font-semibold">{{ chapter.title }}</h4>
                        <NuxtLink
                            v-for="(lesson, index) in chapter.lessons"
                            :key="lesson.slug"
                            class="flex flex-row space-x-1 no-underline prose-sm font-normal text-gray-500 hover:text-gray-900"
                            :to="lesson.path"
                            :class="{
                                'text-blue-500': lesson.path === $route.fullPath,
                                'text-gray-600': lesson.path !== $route.fullPath,
                            }"
                            >
                            <span class="font-semibold">{{ index + 1 }}.</span>
                            <span class="flex-grow">{{ lesson.title }}</span>
                        </NuxtLink>
                    </div>
                </div>
                <div class="w-3/4 mr-6 mt-4 bg-white rounded-md p-5 my-6">
                    <NuxtPage />
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    const { chapters } = useCourse();
</script>

<!-- <style scoped>
    .router-link-active {
        @apply text-blue-500;
    }
</style> -->