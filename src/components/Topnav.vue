<template>
    <div class="topnav">
        <router-link to="/" class="logo">
             <svg class="icon">
                <use xlink:href="#icon-mango33" />
            </svg>
        </router-link>
        <ul class="menu">
            <li>
                <router-link to="/doc">文档</router-link>
            </li>
        </ul>
        <svg v-if="toggleMenuButtonVisible" class="toggleAside" @click="toggleMenu">
            <use xlink:href="#icon-menu" />
        </svg>
    </div>
</template>

<script lang="ts">
import { inject, Ref } from 'vue'


export default {
    props: {
        toggleMenuButtonVisible: {
            type: Boolean,
            default: false,
        }
    },
    setup() {
        const asideVisible = inject<Ref<boolean>>('asideVisible')   //get
        const toggleMenu = () => {
            asideVisible.value = !asideVisible.value
        }
        return { toggleMenu }
    }
}
</script>

<style lang="scss">
$color: #121421;
.topnav {
    background:white;
    color: $color;
    display: flex;
    padding: 16px;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 20;
    justify-content: center;
    align-items: center;
    box-shadow: 0 5px 5px rgb(51 51 51 / 10%);
    > .logo {
        max-width: 6em;
        margin-right: auto;
        > svg {
            width: 34px;
            height: 34px;
        }
    }
    > .menu {
        display: flex;
        white-space: nowrap;
        flex-wrap: nowrap;
        > li {
            margin: 0 1em;
        }
    }
    > .toggleAside {
        width: 28px;
        height: 28px;
        position: absolute;
        left: 16px;
        top: 50%;
        transform: translateY(-50%);
        display: none;
    }
    @media (max-width: 500px) {
        > .menu {
            display: none;
        }
        > .logo {
            margin: 0 auto;
        }
        > .toggleAside {
            display: inline-block;
        }
    }
}
</style>
