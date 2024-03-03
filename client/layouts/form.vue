<template>
    <div>
        <header class="mx-8 mt-8">
            <nav class="flex justify-between text-gray-500">
                <nuxt-link class="decoration-none font-bold tracking-widest text-3xl" to="/">CLIENT</nuxt-link>
            </nav>
        </header>

        <div>
            <slot />
        </div>
    </div>
</template>

<style scoped>
    .router-link-exact-active {
        color: blueviolet;
    }
</style>