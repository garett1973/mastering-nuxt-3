<template>
    <div>
        <p class="mt-0 uppercase font-bold text-slate-400 mb-1">
            Lesson {{ chapter.number }} - {{ lesson.number }}
        </p>
        <h2 class="my-0 text-xl font-semibold">{{ lesson.title }}</h2>
        <div class="flex space-x-4 mt-2 mb-8">
            <NuxtLink
                v-if="lesson.sourceUrl"
                class="font-normal text-md text-gray-500 hover:text-gray-900"
                :to="lesson.sourceUrl"
                >
            Download Source Code
        </NuxtLink>
        <NuxtLink
            v-if="lesson.downloadUrl"
            class="font-normal text-md text-gray-500 hover:text-gray-900"
            :to="lesson.downloadUrl"
            >
            Download Video
        </NuxtLink>
        </div>
        <VideoPlayer v-if="lesson.videoId" :videoId="lesson.videoId" />
        <p class="mb-4">{{ lesson.text }}</p>
            <LessonCompleteButton 
                :model-value="isLessonComplete"
                @update:model-value="toggleComplete"
            />
    </div>
</template>

<script setup>
    const course = useCourse();
    const route = useRoute();

    definePageMeta({
        middleware: function({params}, from) {
            const course = useCourse();

            const chapter = course.chapters.find((chapter) => {
                return chapter.slug === params.chapterSlug;
            });
            
            if (!chapter) {
                return abortNavigation(
                    createError({
                    statusCode: 404,
                    message: 'Chapter not found',
                    })
                );
            }

            const lesson = chapter.lessons.find((lesson) => {
                return lesson.slug === params.lessonSlug;
            });

            if (!lesson) {
                return abortNavigation(
                    createError({
                    statusCode: 404,
                    message: 'Lesson not found',
                    })
                );
            }
        },
    });

    const chapter = computed(() => {
        return course.chapters.find(chapter => chapter.slug === route.params.chapterSlug);
    });

    const lesson = computed(() => {
        return chapter.value.lessons.find(lesson => lesson.slug === route.params.lessonSlug);
    });

    useHead({
        title: `${lesson.value.title} - ${course.title}`,
        meta: [
            {
                hid: 'description',
                name: 'description',
                content: lesson.value.text,
            },
        ],
    });

    // using local storage to preserve the state of lessons
    const progress = useLocalStorage('progress', []);

    const isLessonComplete = computed(() => {
        if (!progress.value[chapter.value.number - 1]) {
            return false;
        }

        if (
            !progress.value[chapter.value.number - 1][
                lesson.value.number - 1
            ]
        ) {
            return false;
        }

        return progress.value[chapter.value.number - 1][
            lesson.value.number - 1
        ];
    });

    const toggleComplete = () => {
        if (!progress.value[chapter.value.number - 1]) {
            progress.value[chapter.value.number - 1] = [];
        }

        progress.value[chapter.value.number - 1][
            lesson.value.number - 1
    ] = !isLessonComplete.value; 
};

</script>