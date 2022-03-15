<template>
  <div
    :class="{
      customer: !customer.isPremium,
      'customer-premium': customer.isPremium,
    }"
    
  >
    <h2>Nome: {{ customer.name }}</h2>
    <h4>E-mail: {{ processEmail(customer.email) }}</h4>
    <h4 v-if="showAge === true">Idade: {{ customer.age }}</h4>
    <h4 v-else>O cliente escondeu a Idade</h4>
    <h6>Descrição: {{ customer.description }}</h6>
    <button class="button is-info" @click="emitEventDelete">Excluir</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isPremium: true,
    };
  },
  props: {
    customer: Object,
    showAge: Boolean,
  },
  methods: {
    emitEventDelete: function () {
      console.log("Emitido do filho!");
      this.$emit("deleteMe", { idCustomer: this.customer.id });
    },
  },
  computed: {
    processEmail() {
      return (value) => {
        return value.toUpperCase();
      };
    },
  },
};
</script>

<style scoped>
.customer {
  background-color: whitesmoke;
  max-width: 600px;
  height: 180px;
  padding: 1%;
  margin-top: 1%;
  text-align: left;
  margin: 1%;
}

.customer-premium {
  background-color: black;
  color: goldenrod;
  max-width: 600px;
  height: 180px;
  padding: 1%;
  margin-top: 1%;
  text-align: left;
  margin: 1%;
}
</style>