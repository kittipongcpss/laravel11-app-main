<script setup>
    import { Head } from '@inertiajs/vue3';
    import SiteLayout from '@/Layouts/SiteLayout.vue';
    defineOptions({ layout: SiteLayout });
</script>

<template>
    <Head title="หน้าหลัก" />

    <div class="p-4 mb-4 text-lg text-center text-blue-800 rounded-lg bg-blue-50 dark:bg-gray-800 dark:text-blue-400" role="alert">
        <span class="font-medium">
           Hello Inertia!
        </span> Change a few things up and try submitting again.
    </div>
</template>
