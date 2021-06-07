<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Supervisor" description="Green Diamond Supervisor Users" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-seller />
                </div>
            </div>
            <div class="ps-section__right">
                <form-seller-create />
            </div>
        </section>
    </div>
</template>
<script>
import TableSeller from "~/components/shared/tables/TableSeller";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormSellerCreate from "~/components/shared/forms/FormSellerCreate";


export default {
    name: "AdministratorScreen",
    components: {
        HeaderDashboard,
        TableSeller,
        FormSearchSimple,
        FormSellerCreate,
    }

}
</script>