<template>
    <div>
        <header class="mx-8 mt-8">
            <nav class="flex justify-between text-gray-500 items-center">
                <NuxtLink class="decoration-none font-bold tracking-widest text-3xl" to="/">CLIENT</NuxtLink>
                <ul>
                    <li class=""><NuxtLink class="px-4 py-2 border border-gray-300 rounded-md" to="/login">Log In</NuxtLink></li>
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