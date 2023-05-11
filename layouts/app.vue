<template>
    <div class="bg-orange-100 min-h-100vh">
        <div class="px-5 pb-6">
            <Nuxt />
        </div>
    </div>
</template>

<script lang="ts" setup></script>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    // async middleware({ redirect, app }) {
    //     const { data } = await app.$supabase.auth.getSession();
    //     if (!data.session) {
    //         redirect("/");
    //     }
    // },
});
</script>
