<template>
    <MainLayout>
        <div class="flex flex-col items-center justify-center h-screen">
            <img src="~/assets/img/JOBARSLogo.png" alt="JOBARS Logo" class="h-50 mb-8">
            <h1 class="text-4xl font-bold mb-4">Welcome to JOBARS EVENTS Events</h1>
            <p class="text-lg mb-8">Catering to Your Dreams, Decorating Your Reality.</p>
        </div>
        <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
            <div>
                <img class="h-auto max-w-full rounded-lg" src="~/assets/img/JOBARS/img1.jpg" alt="">
            </div>
            <div>
                <img class="h-auto max-w-full rounded-lg" src="~/assets/img/JOBARS/img2.jpg" alt="">
            </div>
            <div>
                <img class="h-auto max-w-full rounded-lg" src="~/assets/img/JOBARS/img3.jpg" alt="">
            </div>
            <div>
                <img class="h-auto max-w-full rounded-lg" src="~/assets/img/JOBARS/img4.jpg" alt="">
            </div>
            <div>
                <img class="h-auto max-w-full rounded-lg" src="~/assets/img/JOBARS/img5.jpg" alt="">
            </div>
            <div>
                <img class="h-auto max-w-full rounded-lg" src="~/assets/img/JOBARS/img6.jpg" alt="">
            </div>
        </div>

    </MainLayout>
</template>

<script setup lang="ts">
import MainLayout from "~/layouts/MainLayout.vue";
</script>