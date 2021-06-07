<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Supervisor" description="Green Diamond Supervisor Users" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-supervisor />
                </div>
            </div>
            <div class="ps-section__right">
                <form-supervisor-create />
            </div>
        </section>
    </div>
</template>
<script>
import TableSupervisor from "~/components/shared/tables/TableSupervisor";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormSupervisorCreate from "~/components/shared/forms/FormSupervisorCreate";


export default {
    name: "AdministratorScreen",
    components: {
        HeaderDashboard,
        TableSupervisor,
        FormSearchSimple,
        FormSupervisorCreate,
    }

}
</script>