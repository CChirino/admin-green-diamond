<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Administrator" description="Green Diamond Administrator Users" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-administrator />
                </div>
            </div>
            <div class="ps-section__right">
                <form-administrator-create />
            </div>
        </section>
    </div>
</template>
<script>
import TableAdministrator from "~/components/shared/tables/TableAdministrator";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormAdministratorCreate from "~/components/shared/forms/FormAdministratorCreate";


export default {
    name: "AdministratorScreen",
    components: {
        HeaderDashboard,
        TableAdministrator,
        FormSearchSimple,
        FormAdministratorCreate,
    }

}
</script>