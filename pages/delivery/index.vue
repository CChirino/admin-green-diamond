<template lang="html">
    <div class="ps-page">
        <header-dashboard title="Supervisor" description="Green Diamond Supervisor Users" />
        <section class="ps-dashboard ps-items-listing">
            <div class="ps-section__left">
                <div class="ps-section__header">
                    <form-search-simple />
                </div>
                <div class="ps-section__content">
                    <table-delivery />
                </div>
            </div>
            <div class="ps-section__right">
                <form-delivery-create />
            </div>
        </section>
    </div>
</template>
<script>
import TableDelivery from "~/components/shared/tables/TableDelivery";
import HeaderDashboard from "~/components/shared/headers/HeaderDashboard";
import FormSearchSimple from "~/components/shared/forms/FormSearchSimple";
import FormDeliveryCreate from "~/components/shared/forms/FormDeliveryCreate";


export default {
    name: "DeliveryScreen",
    components: {
        HeaderDashboard,
        TableDelivery,
        FormSearchSimple,
        FormDeliveryCreate,
    }

}
</script>