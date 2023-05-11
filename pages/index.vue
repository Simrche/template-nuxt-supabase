<template>
    <div class="flex flex-col bg-orange-100 h-100vh px-4 w-100vw items-center justify-around">
        <UiTitle size="4xl" class="text-center">Titre</UiTitle>

        <div class="mt-12 w-full">
            <UiButton to="/login">Se connecter</UiButton>
            <UiButton to="/register" class="mt-4">S'inscrire</UiButton>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    name: "IndexPage",
});
</script>
