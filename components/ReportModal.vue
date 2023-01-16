<script>
import DateInput from "./DateInput.vue";

export default {
  name: "ReportModal",
  components: {
    DateInput,
  },
  data() {
    return {
      description: "",
      initDate: null,
      finishDate: null,
      isValidData: false,
    };
  },
  methods: {
    generateReport() {
      this.closeModal();
    },
    submitEvent() {
      // console.log("Descripcion",this.description);
      // console.log("Inicio",this.initDate);
      // console.log("Fin",this.finishDate);
      this.$emit("closeModal");
    },
    closeModal() {
      this.$emit("closeModal");
    },
    validCheck() {
      if (
        this.description &&
        this.initDate &&
        this.finishDate &&
        Date.parse(this.initDate) <= Date.parse(this.finishDate)
      ) {
        this.isValidData = true;
      } else {
        this.isValidData = false;
      }
    },
    updateInitDate(event) {
      this.initDate = event;
      this.validCheck();
    },
    updateFinishDate(event) {
      this.finishDate = event;
      this.validCheck();
    },
  },
  
};
</script>

<template>
  <div class="modal" @click="closeModal()">
      <div
        class="modal-body"
        
        @click.stop
      >
        <h2 class="modal-title">Reporte por fecha de nacimiento</h2>
        <h3 class="modal-subtitle">
          Ingresa los siguientes datos para generar tu reporte
        </h3>
        <form class="modal-content" @submit.prevent="submitEvent()">
          <Input
            label="Descripcion del reporte"
            required
            @input="
              (event) => {
                description = event;
                validCheck();
              }
            "
          />
          <span class="date-label">Fecha de nacimiento</span>
          <div class="input-date">
            <DateInput
              label="Inicio"
              :input-date="initDate"
              :max-date="finishDate"
              :error-max-date="'La fecha inicial es mayor a la final'"
              required
              @update-date="updateInitDate($event)"
              
            />
            <DateInput
              label="Fin"
              :input-date="finishDate"
              :min-date="initDate"
              :error-min-date="'La fecha final es menor a la inicial'"
              required
              @update-date="updateFinishDate($event)"
              
            />
          </div>
          <button :disabled="!isValidData">Generar reporte</button>
        </form>
      </div>
  </div>
</template>

<style lang="scss">
.date-label {
  margin-bottom: 14.5px;
}
</style>
