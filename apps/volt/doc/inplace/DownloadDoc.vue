<template>
    <DocSectionText v-bind="$attrs" />
    <DocSectionCode :code="code" lang="script" />
</template>

<script setup>
import { ref } from 'vue';

const code = ref(`npx volt-vue add inplace
`);
</script>
