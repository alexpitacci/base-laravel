<script setup>
import { useForm, Head, Link } from "@inertiajs/inertia-vue3";
import { mdiAccount, mdiAsterisk } from "@mdi/js";
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
import NotificationBarInCard from "@/Components/NotificationBarInCard.vue";
import BaseLevel from "@/Components/BaseLevel.vue";

const props = defineProps({
    canResetPassword: Boolean,
    status: {
        type: String,
        default: null,
    },
});

const form = useForm({
    email: "",
    password: "",
    remember: [],
});

const submit = () => {
    form.transform((data) => ({
        ...data,
        remember: form.remember && form.remember.length ? "on" : "",
    })).post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};
</script>

<template>
    <LayoutGuest>
        <Head title="Entrar" />

        <SectionFullScreen v-slot="{ cardClass }" bg="purplePink">
            <CardBox :class="cardClass" form @submit.prevent="submit">
                <FormValidationErrors />

                <NotificationBarInCard v-if="status" color="info">
                    {{ status }}
                </NotificationBarInCard>

                <FormField
                    label="E-mail"
                    label-for="email"
                    help="Entre com seu e-mail"
                >
                    <FormControl
                        v-model="form.email"
                        :icon="mdiAccount"
                        id="email"
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
                        :icon="mdiAsterisk"
                        type="password"
                        id="password"
                        autocomplete="current-password"
                        required
                    />
                </FormField>

                <FormCheckRadioGroup
                    v-model="form.remember"
                    name="remember"
                    :options="{ remember: 'Permancecer Conectado' }"
                />

                <BaseDivider />

                <BaseLevel>
                    <BaseButtons>
                        <BaseButton
                            type="submit"
                            color="info"
                            label="Entrar"
                            :class="{ 'opacity-25': form.processing }"
                            :disabled="form.processing"
                        />
                        <BaseButton
                            v-if="canResetPassword"
                            :route-name="route('password.request')"
                            color="info"
                            outline
                            label="Esqueceu a senha?"
                        />
                    </BaseButtons>
                    <Link :href="route('register')"> Registrar </Link>
                </BaseLevel>
            </CardBox>
        </SectionFullScreen>
    </LayoutGuest>
</template>
