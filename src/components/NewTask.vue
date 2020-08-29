<template>
  <div class="new-task">
    <q-input
      @keydown.enter="add"
      type="text"
      filled
      v-model="name"
      label="Adicionar..."
      :dense="dense"
      style="width:80vw"
      color="deep-purple"
    >
      <template v-slot:append>
        <q-btn @click="add" filled dense flat icon="send" />
      </template>
    </q-input>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      dense: false
    }
  },

  methods: {
    add() {
      if (this.name !== '') {
        this.$emit('taskAdded', { name: this.name })
        this.name = ''
      }
    }
  }
}
</script>

<style>
.new-task {
  margin: 35px;
}

.form-element {
  outline: none;
  font-size: 2rem;
  border: 1px solidd #fff;
  padding: 5px 10px 8px;
  color: #fff;
}

input.form-element {
  width: 300px;
  background: #fff2;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

button.form-element {
  border-left: none;
  background-color: #2196f3;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  display: inline;
}
</style>
