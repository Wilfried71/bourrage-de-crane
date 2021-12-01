<template>
  <div class="col-md-12">
    <div class="card p-3">
      <div class="d-flex justify-content-center mb-2">
        {{ currentIndex + 1 }} / {{ data.length }}
      </div>
      <div class="my-4">
        <span style="font-weight: bold" class="h5">
          {{ data[currentIndex].value }}
        </span>
        <input
          type="text"
          class="form-control my-2"
          v-for="(translation, tkey) of data[currentIndex].translations"
          v-model="currentInput[`${tkey}`]"
          :key="tkey"
        />
      </div>
      <div class="d-flex justify-content-center">
        <button class="btn btn-primary mb-2" @click="next">
          Suivant >>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  props: {
    data: [],
    currentIndex: Number,
  },
  data() {
    return {
      currentInput: {}
    }
  },
  methods: {
    next() {
      this.$emit('nextItem', this.currentInput)
      this.currentInput = []
    }
  }
};
</script>

<style scoped>
</style>