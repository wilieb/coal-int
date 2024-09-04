<template>
  <div class="p-4">
    <Header />
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import Header from '../components/Header.vue';
    const config = useRuntimeConfig();
    const auth = btoa(`${config.public.userName}:${config.public.userPassword}`);

    const patientsData = ref([]);

    const getPatients = async () => {
        await $fetch('https://fedskillstest.coalitiontechnologies.workers.dev', {
            method: 'GET',
            headers: { 'Authorization': `Basic ${auth}` },
            onResponse: ({ response }) => {
                if (response.status === 200) {
                    patientsData.value = response._data;
                }
            }
        });
    };

    onMounted(() => {
        getPatients();
    });
</script>

<style>

</style>