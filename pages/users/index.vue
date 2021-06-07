<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Users" description="Green Diamond Users Listing" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-users />
                </div>
            </div>
            <div class="ps-section__right">
                <form-users-create />
            </div>
        </section>
    </div>
</template>
<script>
import TableUsers from "~/components/shared/tables/TableUsers";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormUsersCreate from "~/components/shared/forms/FormUserCreate";


export default {
    name: "UsersScreen",
    components: {
        HeaderDashboard,
        TableUsers,
        FormSearchSimple,
        FormUsersCreate,
    }

}
</script>