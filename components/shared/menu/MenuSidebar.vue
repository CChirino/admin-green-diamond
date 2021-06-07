<template lang="html">
    <ul class="menu">
        <li v-for="item in menuItems" :key="item.text">
            <nuxt-link :to="item.url" class="menu__text">
                <i :class="item.icon"> </i>
                <span>{{ item.text }}</span>
            </nuxt-link>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'MenuSidebar',
    data() {
        return {
            menuItems: [
                {
                    text: 'Dashboard',
                    url: '/',
                    icon: 'icon-home'
                },
                {
                    text: 'Users',
                    url: '/users',
                    icon: 'icon-users2'
                },
                {
                    text: 'Administrator',
                    url: '/administrator',
                    icon: 'icon-users2'
                },
                {
                    text: 'Seller',
                    url: '/seller',
                    icon: 'icon-users2'
                },
                {
                    text: 'Delivery',
                    url: '/delivery',
                    icon: 'icon-users2'
                },
                {
                    text: 'Super Administrator',
                    url: '/super-administrator',
                    icon: 'icon-users2'
                },
                {
                    text: 'Supervisor',
                    url: '/supervisor',
                    icon: 'icon-users2'
                },
                {
                    text: 'Roles',
                    url: '/roles',
                    icon: 'icon-users2'
                },
                {
                    text: 'Permission',
                    url: '/permission',
                    icon: 'icon-users2'
                },
                {
                    text: 'Products',
                    url: '/products',
                    icon: 'icon-database'
                },
                {
                    text: 'Orders',
                    url: '/orders',
                    icon: 'icon-bag2'
                },
                {
                    text: 'Customers',
                    url: '/customers',
                    icon: 'icon-users2'
                },
                {
                    text: 'Categories',
                    url: '/categories',
                    icon: 'icon-users2'
                },
                {
                    text: 'Settings',
                    url: '/settings',
                    icon: 'icon-cog'
                }
            ]
        };
    }
};
</script>

<style lang="scss" scoped></style>
