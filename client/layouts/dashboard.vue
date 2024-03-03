<template>
    <div div v-if="isAuthenticated">
        <header class="mx-8 mt-8">
            <nav class="flex justify-between text-gray-500 items-center">
                <nuxt-link class="decoration-none font-bold tracking-widest text-3xl" to="/dashboard">DASHBOARD</nuxt-link>
                <ul>
                    <li class=""><button @click="logout" class="px-4 py-2 border border-gray-300 rounded-md">Log Out</button></li>
                </ul>
            </nav>
        </header>

        <div>
            <slot />
        </div>
    </div>

    <div v-else>
        <main class="mx-8 mt-8 flex text-gray-500 items-center justify-center h-[90vh]">
            <p>Please <nuxt-link class="text-blue-500 font-bold" to="/login">log in </nuxt-link>to access the dashboard.</p>
        </main>
    </div>
</template>

<script setup>
    const isAuthenticated = ref(false);
    const route = useRoute();
    const router = useRouter();

    onMounted(() => {
        checkAuthentication();
    });

    function checkAuthentication() {
        if (localStorage.getItem('_token')) {
            isAuthenticated.value = true;
        } else {
            isAuthenticated.value = false;

        }
    }

    function logout() {
        localStorage.removeItem('_token');
        router.push('/');
    }

    router.beforeEach((to, from, next) => {
        if (from.path === '/dashboard' && isAuthenticated.value) {
            localStorage.removeItem('_token');
        }
        next();
    });
</script>

<style scoped>
    .router-link-exact-active {
        color: blueviolet;
    }
</style>