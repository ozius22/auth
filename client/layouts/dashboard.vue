<template>
    <div>
        <header class="mx-8 mt-8">
            <nav class="flex justify-between text-gray-500 items-center">
                <nuxt-link class="decoration-none font-bold tracking-widest text-3xl" to="/dashboard">DASHBOARD</nuxt-link>
                <ul>
                    <li class=""><nuxt-link class="px-4 py-2 border border-gray-300 rounded-md" to="/">Log Out</nuxt-link></li>
                </ul>
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