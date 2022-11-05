<script setup>
import { useForm, Head, Link } from "@inertiajs/inertia-vue3";
import { mdiEmail, mdiFormTextboxPassword } from "@mdi/js";
import LayoutGuest from "@/Layouts/LayoutGuest.vue";
import SectionFullScreen from "@/Components/SectionFullScreen.vue";
import CardBox from "@/Components/CardBox.vue";
import FormField from "@/Components/FormField.vue";
import FormControl from "@/Components/FormControl.vue";
import BaseDivider from "@/Components/BaseDivider.vue";
import BaseButton from "@/Components/BaseButton.vue";
import FormValidationErrors from "@/Components/FormValidationErrors.vue";

const props = defineProps({
    email: {
        type: String,
        default: null,
    },
    token: {
        type: String,
        default: null,
    },
});

const form = useForm({
    token: props.token,
    email: props.email,
    password: "",
    password_confirmation: "",
});

const submit = () => {
    form.post(route("password.update"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <LayoutGuest>
        <Head title="Reiniciar a Senha" />

        <SectionFullScreen v-slot="{ cardClass }" bg="purplePink">
            <CardBox :class="cardClass" form @submit.prevent="submit">
                <FormValidationErrors />

                <FormField
                    label="E-mail"
                    label-for="email"
                    help="Entre com seu e-mail"
                >
                    <FormControl
                        v-model="form.email"
                        :icon="mdiEmail"
                        autocomplete="email"
                        type="email"
                        id="email"
                        required
                    />
                </FormField>

                <FormField
                    label="Senha"
                    label-for="password"
                    help="Entre com a Senha"
                >
                    <FormControl
                        v-model="form.password"
                        :icon="mdiFormTextboxPassword"
                        type="password"
                        autocomplete="new-password"
                        id="password"
                        required
                    />
                </FormField>

                <FormField
                    label="Confirme a Senha"
                    label-for="password_confirmation"
                    help="Confirme a nova senha"
                >
                    <FormControl
                        v-model="form.password_confirmation"
                        :icon="mdiFormTextboxPassword"
                        type="password"
                        autocomplete="new-password"
                        id="password_confirmation"
                        required
                    />
                </FormField>

                <BaseDivider />

                <BaseButton
                    type="submit"
                    color="info"
                    label="Salvar nova Senha"
                    :class="{ 'opacity-25': form.processing }"
                    :disabled="form.processing"
                />
            </CardBox>
        </SectionFullScreen>
    </LayoutGuest>
</template>
