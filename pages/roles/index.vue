<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Roles" description="Green Diamond Roles Listing" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-roles />
                </div>
            </div>
            <div class="ps-section__right">
                <form-role-create />
            </div>
        </section>
    </div>
</template>
<script>
import TableRoles from "~/components/shared/tables/TableRoles";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormRoleCreate from "~/components/shared/forms/FormRoleCreate";
export default {
    name: "RolesScreen",
    components: {
        HeaderDashboard,
        TableRoles,
        FormSearchSimple,
        FormRoleCreate,
    }

}
</script>