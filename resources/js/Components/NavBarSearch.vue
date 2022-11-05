<script setup>
import FormControl from "@/Components/FormControl.vue";
</script>

<template>
    <FormControl
        ref="root"
        placeholder="Pesquisar (ctrl+k)"
        ctrl-k-focus
        transparent
        borderless
    />
</template>
