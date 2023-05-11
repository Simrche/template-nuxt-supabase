<template>
    <div v-if="!created" class="flex flex-col bg-orange-100 h-100vh px-4 w-100vw items-center justify-around">
        <UiTitle size="4xl" class="text-center">Titre</UiTitle>
        <div class="w-full">
            <UiInput label="Nom d'utilisateur" class="mt-4" v-model="credentials.username"></UiInput>
            <p class="mt-1 text-sm text-red-500" v-if="requiredFields.username">
                Une nom d'utilisateur doit être renseignée
            </p>
            <UiInput label="Email" class="mt-4" v-model="credentials.email"></UiInput>
            <p class="mt-1 text-sm text-red-500" v-if="requiredFields.email">Une email doit être renseignée</p>
            <UiInput label="Mot de passe" class="mt-4" type="password" v-model="credentials.password"></UiInput>
            <p class="mt-1 text-sm text-red-500" v-if="requiredFields.password">
                Une mot de passe doit être renseignée
            </p>
            <UiInput
                label="Confirmation du mot de passe"
                class="mt-4"
                type="password"
                v-model="credentials.confirmPassword"
            ></UiInput>
            <p class="mt-1 text-sm text-red-500" v-if="requiredFields.confirmPassword">
                Les mots de passe ne correspondent pas
            </p>
        </div>
        <div class="w-full">
            <UiButton @click="register()">S'inscrire</UiButton>
            <router-link to="/login" class="text-xs">Vous avez déjà un compte ? Se connecter</router-link>
        </div>
    </div>
    <div v-else class="flex bg-orange-100 h-100vh px-4 w-100vw items-center justify-center">
        <UiTitle class="text-center">Veuillez vérifer votre email afin d'accéder au Dashboard</UiTitle>
    </div>
</template>

<script setup lang="ts">
const supabase = useSupabase();
const router = useRouter();

const created = ref(false);

const credentials = ref({
    username: "",
    email: "",
    password: "",
    confirmPassword: "",
});

const requiredFields = ref({
    username: false,
    email: false,
    password: false,
    confirmPassword: false,
});

async function register() {
    requiredFields.value = {
        username: false,
        email: false,
        password: false,
        confirmPassword: false,
    };

    checkFields();

    if (Object.values(requiredFields.value).some(field => field)) return;

    // TODO Validation fields

    const { data, error } = await supabase.auth.signUp({
        email: credentials.value.email,
        password: credentials.value.password,
        options: {
            data: {
                username: credentials.value.username,
            },
        },
    });

    if (error) {
        // TODO display error
    } else {
        created.value = true;
    }
}

function checkFields() {
    if (credentials.value.password !== credentials.value.confirmPassword) requiredFields.value.confirmPassword = true;
    if (!credentials.value.username) requiredFields.value.username = true;
    if (!credentials.value.email) requiredFields.value.email = true;
    if (!credentials.value.password) requiredFields.value.password = true;
}
</script>

<script lang="ts">
import { ref, useRouter } from "@nuxtjs/composition-api";
import { defineComponent } from "vue";
import { useSupabase } from "~/utils";

export default defineComponent({
    // async middleware({ redirect, app }) {
    //     const { data } = await app.$supabase.auth.getSession();
    //     if (data.session) {
    //         redirect("/dashboard");
    //     }
    // },
});
</script>
