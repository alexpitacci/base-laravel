<script setup>
import { Head, Link, useForm } from "@inertiajs/inertia-vue3";
import { mdiAccountKey, mdiArrowLeftBoldOutline } from "@mdi/js";
import LayoutAuthenticated from "@/Layouts/LayoutAuthenticated.vue";
import SectionMain from "@/Components/SectionMain.vue";
import SectionTitleLineWithButton from "@/Components/SectionTitleLineWithButton.vue";
import CardBox from "@/Components/CardBox.vue";
import BaseButton from "@/Components/BaseButton.vue";

const props = defineProps({
    role: {
        type: Object,
        default: () => ({}),
    },
    permissions: {
        type: Object,
        default: () => ({}),
    },
    roleHasPermissions: {
        type: Object,
        default: () => ({}),
    },
});
</script>

<template>
    <LayoutAuthenticated>
        <Head title="Ver role" />
        <SectionMain>
            <SectionTitleLineWithButton
                :icon="mdiAccountKey"
                title="Ver role"
                main
            >
                <BaseButton
                    :route-name="route('role.index')"
                    :icon="mdiArrowLeftBoldOutline"
                    label="Voltar"
                    color="white"
                    rounded-full
                    small
                />
            </SectionTitleLineWithButton>
            <CardBox class="mb-6">
                <table>
                    <tbody>
                        <tr>
                            <td
                                class="p-4 pl-8 text-slate-500 dark:text-slate-400 hidden lg:block"
                            >
                                Nome
                            </td>
                            <td data-label="Nome">
                                {{ role.name }}
                            </td>
                        </tr>
                        <tr>
                            <td
                                class="p-4 pl-8 text-slate-500 dark:text-slate-400 hidden lg:block"
                            >
                                Criado em
                            </td>
                            <td data-label="Criado em">
                                {{ new Date(role.created_at).toLocaleString() }}
                            </td>
                        </tr>
                    </tbody>
                </table>
            </CardBox>
        </SectionMain>
    </LayoutAuthenticated>
</template>
