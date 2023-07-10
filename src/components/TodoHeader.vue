<template>
    <div>
        <header>
            <nav class="container">
                <div class="branding">
                    <img src="@/assets/Vue_Logo_Black.png" />
                    <h1>Vue Todos</h1>
                </div>
                <ul class="nav-routes">
                    <RouterLink to="/">Home</RouterLink>
                    <RouterLink to="/about">About</RouterLink>
                </ul>
            </nav>
        </header>
    </div>
</template>

<script setup>
import { RouterLink } from "vue-router"
</script>

<style lang="scss" scoped>
header {
    background-color: #f1f1f1;

    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 25px 16px;

        .branding {
            display: flex;
            align-items: center;
            gap: 8px;

            img {
                max-width: 50px;
            }

            h1 {
                font-size: 24px;
            }
        }

        .nav-routes {
            display: flex;
            gap: 5px;
            justify-content: flex-end;

            a {
                text-decoration: none;
                color: inherit;
            }
        }
    }
}
</style>