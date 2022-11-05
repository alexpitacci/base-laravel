<script setup>
import { useForm, usePage, Head } from "@inertiajs/inertia-vue3";
import { computed } from "vue";
import { mdiAccount, mdiEmail, mdiFormTextboxPassword } from "@mdi/js";
import LayoutGuest from "@/Layouts/LayoutGuest.vue";
import SectionFullScreen from "@/Components/SectionFullScreen.vue";
import CardBox from "@/Components/CardBox.vue";
import FormCheckRadioGroup from "@/Components/FormCheckRadioGroup.vue";
import FormField from "@/Components/FormField.vue";
import FormControl from "@/Components/FormControl.vue";
import BaseDivider from "@/Components/BaseDivider.vue";
import BaseButton from "@/Components/BaseButton.vue";
import BaseButtons from "@/Components/BaseButtons.vue";
import FormValidationErrors from "@/Components/FormValidationErrors.vue";

const form = useForm({
    name: "",
    email: "",
    password: "",
    password_confirmation: "",
    terms: [],
});

const hasTermsAndPrivacyPolicyFeature = computed(
    () => usePage().props.value?.jetstream?.hasTermsAndPrivacyPolicyFeature
);

const submit = () => {
    form.transform((data) => ({
        ...data,
        terms: form.terms && form.terms.length,
    })).post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <LayoutGuest>
        <Head title="Registrar" />

        <SectionFullScreen v-slot="{ cardClass }" bg="purplePink">
            <CardBox
                :class="cardClass"
                class="my-24"
                form
                @submit.prevent="submit"
            >
                <FormValidationErrors />

                <FormField
                    label="Nome"
                    label-for="name"
                    help="Entre com o seu nome"
                >
                    <FormControl
                        v-model="form.name"
                        id="name"
                        :icon="mdiAccount"
                        autocomplete="name"
                        type="text"
                        required
                    />
                </FormField>

                <FormField
                    label="E-mail"
                    label-for="email"
                    help="Entre com o seu e-mail"
                >
                    <FormControl
                        v-model="form.email"
                        id="email"
                        :icon="mdiEmail"
                        autocomplete="email"
                        type="email"
                        required
                    />
                </FormField>

                <FormField
                    label="Senha"
                    label-for="password"
                    help="Entre com a sua senha"
                >
                    <FormControl
                        v-model="form.password"
                        id="password"
                        :icon="mdiFormTextboxPassword"
                        type="password"
                        autocomplete="new-password"
                        required
                    />
                </FormField>

                <FormField
                    label="Confirme a Senha"
                    label-for="password_confirmation"
                    help="Digite a senha novamente"
                >
                    <FormControl
                        v-model="form.password_confirmation"
                        id="password_confirmation"
                        :icon="mdiFormTextboxPassword"
                        type="password"
                        autocomplete="new-password"
                        required
                    />
                </FormField>

                <FormCheckRadioGroup
                    v-if="hasTermsAndPrivacyPolicyFeature"
                    v-model="form.terms"
                    name="remember"
                    :options="{ agree: 'Concordo com os Termos' }"
                />

                <BaseDivider />

                <BaseButtons>
                    <BaseButton
                        type="submit"
                        color="info"
                        label="Register"
                        :class="{ 'opacity-25': form.processing }"
                        :disabled="form.processing"
                    />
                    <BaseButton
                        :route-name="route('login')"
                        color="info"
                        outline
                        label="Entrar"
                    />
                </BaseButtons>
            </CardBox>
        </SectionFullScreen>
    </LayoutGuest>
</template>
