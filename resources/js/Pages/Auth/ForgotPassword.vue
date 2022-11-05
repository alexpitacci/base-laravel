<script setup>
import { useForm, Head, Link } from "@inertiajs/inertia-vue3";
import { mdiEmail } from "@mdi/js";
import LayoutGuest from "@/Layouts/LayoutGuest.vue";
import SectionFullScreen from "@/Components/SectionFullScreen.vue";
import CardBox from "@/Components/CardBox.vue";
import FormField from "@/Components/FormField.vue";
import FormControl from "@/Components/FormControl.vue";
import BaseDivider from "@/Components/BaseDivider.vue";
import BaseButton from "@/Components/BaseButton.vue";
import FormValidationErrors from "@/Components/FormValidationErrors.vue";
import NotificationBarInCard from "@/Components/NotificationBarInCard.vue";
import BaseLevel from "@/Components/BaseLevel.vue";

defineProps({
    status: {
        type: String,
        default: null,
    },
});

const form = useForm({
    email: "",
});

const submit = () => {
    form.post(route("password.email"));
};
</script>

<template>
    <LayoutGuest>
        <Head title="Forgot Password" />

        <SectionFullScreen v-slot="{ cardClass }" bg="purplePink">
            <CardBox :class="cardClass" form @submit.prevent="submit">
                <FormValidationErrors />

                <NotificationBarInCard v-if="status" color="info">
                    {{ status }}
                </NotificationBarInCard>

                <FormField>
                    <div class="mb-4 text-sm text-gray-600">
                        Esqueceu a sua senha? Sem problemas. Informe a seu
                        e-mail que mandamos um link pra você reiniciar a sua
                        senha.
                    </div>
                </FormField>

                <FormField label="E-mail" help="Entre seu E-mail">
                    <FormControl
                        v-model="form.email"
                        :icon="mdiEmail"
                        autocomplete="email"
                        type="email"
                        required
                    />
                </FormField>

                <BaseDivider />

                <BaseLevel>
                    <BaseButton
                        type="Salvar"
                        color="info"
                        label="Email link"
                        :class="{ 'opacity-25': form.processing }"
                        :disabled="form.processing"
                    />
                    <Link :href="route('login')"> Voltar para o login </Link>
                </BaseLevel>
            </CardBox>
        </SectionFullScreen>
    </LayoutGuest>
</template>
