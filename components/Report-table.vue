<script>
export default {
  props: {
    reports: {
      type: Array,
      default: [],
    },
  },
};
</script>
<template>
  <div class="table-background">
    <table>
      <thead>
        <tr>
          <th>Titulo</th>
          <th></th>
          <th>Fecha de creación</th>
          <th></th>
          <th>Acción</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="report in reports">
          <td>{{ report.title }}</td>
          <td class="separator"><div class="separator-line"></div></td>
          <td>{{ report.creation }}</td>
          <td class="separator"><div class="separator-line"></div></td>
          <td>
            <a :href="report.download">
              Descargar
              <img src="../assets/svgs/download-icon.svg" alt="download icon" />
            </a>
          </td>
        </tr>
      </tbody>
    </Table>
  </div>
</template>
