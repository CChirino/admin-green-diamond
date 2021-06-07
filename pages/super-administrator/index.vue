<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Super-Administrator" description="Green Diamond Super-Administrator Users" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-super-administrator />
                </div>
            </div>
            <div class="ps-section__right">
                <form-super-administrator-create />
            </div>
        </section>
    </div>
</template>
<script>
import TableSuperAdministrator from "~/components/shared/tables/TableSuperAdministrator";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormSuperAdministratorCreate from "~/components/shared/forms/FormSuperAdministratorCreate";


export default {
    name: "SuperAdministratorScreen",
    components: {
        HeaderDashboard,
        TableSuperAdministrator,
        FormSearchSimple,
        FormSuperAdministratorCreate,
    }

}
</script>