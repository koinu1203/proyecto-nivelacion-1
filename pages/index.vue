<template>
  <div>
    <transition name="modal">
      <ReportModal 
      v-if="showModal"
                   @closeModal="() => (showModal = false)" />
    </transition>
    <section>
      <h1>Generador de reportes</h1>
      <Report-table :reports="reports" />
      <button 
      id="open-report-modal"
              @click="showModal = true">
        Crear reporte
      </button>
    </section>
  </div>
</template>

<script>
import ReportModal from "@/components/ReportModal.vue";
const getResportList = () => import('@/static/json/report-list.json').then(m=>m.default || m)

export default {
  name: "LandingPage",
  components: {
    ReportModal,
  },
  data() {
    return {
      showModal: false,
      reports: null
    };
  },
  created() {
    this.getReports();
  },
  methods: {
    async getReports() {
      try{
        const res = await getResportList();
        this.reports = res.reports;
      }catch(e){
        // console.error(e);
      }

    }
  },
};
</script>
