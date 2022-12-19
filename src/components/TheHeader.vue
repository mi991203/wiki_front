<template>
    <a-layout-header class="header">
        <div class="logo">
            <img src="../assets/logo.png">
        </div>
        <a-menu
                v-model:selectedKeys="selectedKeys1"
                theme="dark"
                mode="horizontal"
                :style="{ lineHeight: '64px' }"
        >
            <a-menu-item key="/">
                <router-link to="/">Home</router-link>
            </a-menu-item>
            <a-menu-item key="/about">
                <router-link to="/about">About</router-link>
            </a-menu-item>
        </a-menu>
    </a-layout-header>
</template>

<script lang="ts">
    import {defineComponent} from 'vue';

    export default defineComponent({
        name: 'the-header'
    });
</script>

<style scoped>

    .header {
        padding: 0;
    }

    .header .logo {
        width: 200px;
        float: left;
    }

    .header .logo img {
        width: 30px;
        height: 30px;
        margin: 0 85px;
    }

    a-menu {
        /*float: left;*/
        margin-left: 200px;
    }
</style>