<template>
  <div
    class="flex-column d-flex justify-content-center align-items-center vh-100 vw-100"
    :style="{ backgroundColor: this.color }"
  >
    <div class="d-flex">
      <div
        class="m-3 p-2 card border-dark text-center bg-transparent font-weight-bolder"
      >
        <h4>Se te da la bienvenida</h4>
        <p>
          Presiona el botón para que se te asigne un color, ojo, solo podras
          hacerlo una sola vez.
        </p>
      </div>
      <div>
      </div>
    </div>
    <div class="card border w-75 h-75">
      <div class="card-header h-100">
        <div class="card body h-100 justify-content-center bg-white">
          <div
            class="d-flex flex-column justify-content-center align-items-center"
          >
            <CounterComponent
              :disabled-button="disabledButton"
              :color="color"
              :count="count"
              :random-number="randomNumber"
              @touch-ok="pressOk"
            />
            <ChartComponent v-if="showChart" class="w-50" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ChartComponent from "./components/ChartComponent.vue";
import CounterComponent from "./components/CounterComponent.vue";

export default {
  components: {
    CounterComponent,
    ChartComponent,
  },
  data() {
    return {
      disabledButton: false,
      color: "",
      showChart: false,
      count: 60,
      randomNumber: 0,
    };
  },
  methods: {
    // Una vez presionado el Ok el boton asignamos un color determinado dependiendo de la cantidad de segundos que hayan pasado
    pressOk(count, color) {
      if (count >= 52) {
        color = "violet";
      } else if (count <= 51 && count >= 42) {
        color = "blue";
      } else if (count <= 41 && count >= 32) {
        color = "green";
      } else if (count <= 31 && count >= 22) {
        color = "yellow";
      } else if (count <= 21 && count >= 12) {
        color = "orange";
      } else if (count <= 11 && count >= 1) {
        color = "red";
      }
      localStorage.setItem("color", color);
      this.color = localStorage.getItem("color");
      this.showChart = true;
      this.disabledButton = true;
    },
    getRandomNumber() {
      return Math.floor(Math.random() * 60);
    },
  },
  mounted() {
    // Se setea el numero aleatorio apenas se entra a la pagina
    this.randomNumber = this.getRandomNumber();
    this.color = localStorage.getItem("color") || "";
    setInterval(() => {
      if (this.count > 0) {
        this.count--;
        // En el caso de que el numero aleatorio sea 0 se le asignara el color que corresponde (gris)
        if (this.count == 0 && localStorage.getItem("color") === '') {
          this.color = "grey";
          localStorage.setItem("color", this.color);
          this.showChart = true;
          this.disabledButton = true;
        }
        // En caso de que el numero del contador sea igual al numero aleatorio se volvera el contador a 60 asignandole al
        // mismo tiempo un nuevo numero aleatorio
        if (this.randomNumber === this.count) {
          this.count = 60;
          this.randomNumber = this.getRandomNumber();
        }
      }
    }, 1000);
    if (this.color === "") {
      this.showChart = false;
      this.disabledButton = false;
    } else {
      this.showChart = true;
      this.disabledButton = true;
    }
  },
};
</script>
