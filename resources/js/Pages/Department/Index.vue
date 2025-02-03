<script setup>
    import { Head, Link, usePage, router } from '@inertiajs/vue3';
    import {useToast} from 'vue-toast-notification';
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    import { onMounted } from 'vue';

    defineOptions({ layout: AuthenticatedLayout });

    defineProps({
        departments: Array
    });

    const toast = useToast();
    const page = usePage();

    onMounted(() => {
        if (page.props.flash.message) {
            toast.success(page.props.flash.message);
        }
    })

    const onHandleDelete = (id) => {
        if (confirm('แน่ใจว่าต้องการลบข้อมูลนี้')) {
            router.delete('/dashboard/department/destroy', {
                data: {id: id},
                onSuccess: (page) => {
                    toast.success(page.props.flash.message);
                }
            });
        }
    }

</script>

<template>

<Head title="Department" />


<div class="relative overflow-x-auto">
    <div class="mx-auto mt-4 max-w-7xl sm:px-6 lg:px-8">

    <Link :href="route('department.create')" class=" text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 text-center me-2 mb-5 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">เพิ่มข้อมูล</Link>


    <table class="w-full mt-5 text-sm text-left text-gray-500 rtl:text-right dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6 py-3">
                    ID
                </th>
                <th scope="col" class="px-6 py-3">
                    Name
                </th>
                <th scope="col" class="px-6 py-3">
                    Created At
                </th>
                <th scope="col" class="px-6 py-3">
                    Actions
                </th>
            </tr>
        </thead>
        <tbody>

            <tr v-for="item in departments" :key="item.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    {{ item.id }}
                </th>
                <td class="px-6 py-4">
                    {{ item.name }}
                </td>
                <td class="px-6 py-4">
                    {{ new Date(item.created_at).toLocaleDateString('th-TH') }}
                </td>
                <td class="px-6 py-4">
                    <a :href="route('department.edit', {id: item.id})" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
                    |
                    <a @click="onHandleDelete(item.id)" href="#" class="font-medium text-red-600 cursor-pointer dark:text-red-500 hover:underline">Delete</a>
                </td>
            </tr>

        </tbody>
    </table>

</div>
</div>

</template>
