<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Permission" description="Permission Module" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-permission />
                </div>
            </div>
            <div class="ps-section__right">
                <form-permission-create />
            </div>
        </section>
    </div>
</template>
<script>
import TablePermission from "~/components/shared/tables/TablePermission";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormPermissionCreate from "~/components/shared/forms/FormPermissionCreate";


export default {
    name: "PermissionScreen",
    components: {
        HeaderDashboard,
        TablePermission,
        FormSearchSimple,
        FormPermissionCreate,
    }

}
</script>