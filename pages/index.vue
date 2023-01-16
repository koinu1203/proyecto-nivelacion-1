<template>
  <div>
    <Transition name="modal">
      <ReportModal 
      v-if="showModal"
                   @closeModal="() => (showModal = false)" />
    </Transition>
    <Header />
    <section>
      <h1>Generador de reportes</h1>
      <ReportTable />
      <button 
      id="open-report-modal"
              @click="showModal = true">
        Crear reporte
      </button>
    </section>
  </div>
</template>

<script>
import ReportTable from "@/components/Table.vue";
import ReportModal from "@/components/ReportModal.vue";
export default {
  name: "LandingPage",
  components: {
    ReportModal,
    ReportTable,
  },
  data() {
    return {
      showModal: false,
    };
  },
};
</script>
