<template>
  <div class="row mt-3">
    <div class="col">
      <div class="card border border-dark">
        <div class="card-header">
          <div class="card body">
            <Bar :options="chartOptions" :data="chartData" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Bar } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
);

export default {
  name: "BarChart",
  components: { Bar },
  props: {
    chartId: {
      type: String,
      default: "bar-chart",
    },
  },
  data() {
    return {
      chartData: {
        labels: [
          "Purpura",
          "Azul",
          "Verde",
          "Amarillo",
          "Naranja",
          "Rojo",
          "Gris",
        ],
        // Aca simulamos una estadistica de los clicks de los usuarios con sus respectivos colores.
        datasets: [
          {
            label: "Usuarios",
            data: [66, 48, 76, 21, 63, 15, 19],
            backgroundColor: [
              "purple",
              "blue",
              "green",
              "yellow",
              "orange",
              "red",
              "grey",
            ],
          },
        ],
      },
      chartOptions: {
        responsive: true,
      },
    };
  },
};
</script>
