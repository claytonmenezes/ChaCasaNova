<template>
  <div class="notebook-page">
    <textarea v-model="textContent" class="notebook-textarea"></textarea>
  </div>
</template>

<script>
export default {
  name: 'FolhaDeCaderno',
  props: {
    modelValue: {
      type: String,
      default: ''
    }
  },
  computed: {
    textContent: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit('update:modelValue', value);
      }
    }
  }
};
</script>

<style scoped>
/* Estilo geral da página do caderno */
.notebook-page {
  position: relative;
  background-color: #fdfdfd;
  margin: 1rem auto;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.2);
  overflow: hidden;
}

/* Linhas horizontais simulando uma folha de caderno */
.notebook-page::before {
  content: "";
  position: absolute;
  top: 1rem;
  left: 0.5rem;
  width: calc(100% - 0.5rem);
  height: 100%;
  background-image: repeating-linear-gradient(
    to bottom,
    #e0e0e0 0px,
    #e0e0e0 1px,
    transparent 1px,
    transparent 30px
  );
  pointer-events: none;
  z-index: 1;
}

/* Bordas perfuradas na lateral esquerda */
.notebook-page::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 0.5rem;
  height: 100%;
  background-image: radial-gradient(circle, #ccc 2px, transparent 2px);
  background-size: 8px 30px;
  z-index: 1;
}

/* Estilo do textarea com linhas e bordas */
.notebook-textarea {
  position: relative;
  z-index: 2;
  background: transparent;
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  resize: none;
  font-size: 1rem;
  line-height: 1.9rem;
  padding-left: 0.5rem;
  color: #333;
}
</style>
