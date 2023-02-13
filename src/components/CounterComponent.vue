<template>
  <div>
    <h1 class="text-center font-weight-bold font-size-xl" :style="{color: color}">{{ count }}</h1>
    <b-button
      :style="{ backgroundColor: color }"
      :disabled = disabledButton
      v-b-modal.modal
      size="lg"
      class="font-weight-bold border"
      pill
      @click="getCountAlert"
      >Click Aqui</b-button
    >
    <b-modal id="modal" title="Confirmar" @ok="pressOk">
      <p class="my-4">
        Quieres presionar el boton en el segundo {{ this.countAlert }} ?
      </p>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    disabledButton: Boolean,
    color: String,
    count: Number,
    randomNumber: Number
  },
  data() {
    return {
      countAlert: 0
    };
  },
  methods: {
    getCountAlert() {
      this.countAlert = this.count
    },
    pressOk() {
      this.$emit("touch-ok", this.count, this.color);
    },
  },
};
</script>