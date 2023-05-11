<template>
    <div class="flex flex-col bg-orange-100 h-100vh px-4 w-100vw items-center justify-around">
        <UiTitle size="4xl" class="text-center">Titre</UiTitle>
        <div class="w-full">
            <UiInput label="Nom d'utilisateur" v-model="credentials.email" @input="showErrorMessage = false"></UiInput>
            <UiInput
                label="Mot de passe"
                class="mt-4"
                type="password"
                v-model="credentials.password"
                @input="showErrorMessage = false"
            ></UiInput>
            <p class="mt-4 text-sm text-red-500" v-if="showErrorMessage">Informations de connexion incorrect</p>
        </div>
        <div class="w-full">
            <UiButton @click="login()">Se connecter</UiButton>
            <router-link to="/register" class="text-xs">Vous n'avez pas de compte ? S'inscrire </router-link>
        </div>
    </div>
</template>

<script setup lang="ts">
const supabase = useSupabase();
const router = useRouter();

const showErrorMessage = ref(false);

const credentials = ref({
    email: "",
    password: "",
});

async function login() {
    const { error } = await supabase.auth.signInWithPassword(credentials.value);

    if (error) {
        console.log(error);
        // TODO display error
        showErrorMessage.value = true;
    } else {
        router.push("/dashboard");
    }
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
