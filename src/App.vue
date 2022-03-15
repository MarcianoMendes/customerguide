<template>
  <div id="app">
    <h1>Guia Clientes</h1>
      <div class="sizebox box">
        <div class="tile">
          <label class="label">Cadastro</label>
        </div>
        <small id="errorName" v-show="occurredError"
          >O nome deve ser informado com mais de 3 caracteres</small
        ><br />
        <div class="field">
          <label class="tile">Nome</label>
          <div class="control">
            <input
              class="input"
              type="text"
              placeholder="Nome"
              v-model="nameField"
            />
          </div>
        </div>

        <div class="field">
          <label class="tile">Email</label>
          <div class="control">
            <input
              class="input"
              type="email"
              placeholder="E-mail"
              v-model="emailField"
            />
          </div>
        </div>

        <div class="field">
          <label class="tile">Idade</label>
          <div class="control">
            <input
              class="input"
              type="number"
              placeholder="Idade"
              v-model="ageField"
            />
          </div>
        </div>

        <div class="field">
          <label class="tile">Descrição</label>
          <div class="control">
            <input
              class="input"
              type="text"
              placeholder="Descrição"
              v-model="descriptionField"
            />
          </div>
        </div>
        <div class="tile" >
          <input id="cbxPremium" type="checkbox" v-model="isPremiumField" />
          <label for="cbxPremium">Premium</label>
        </div>

        <button class="button is-dark" @click="registerCustomer">
          Cadastrar
        </button>
      </div>
    <div v-for="(customer, index) in orderCustumers" :key="customer.id">
      <h4 style="text-align: left">{{ index + 1 }}</h4>
      <Customer :customer="customer" @deleteMe="deleteCustomer($event)" />
    </div>
  </div>
</template>

<script>
import _ from "lodash";
import Customer from "./components/CustomerItem";
// import Product from './components/ProductItem'
export default {
  name: "App",
  data() {
    return {
      occurredError: false,
      isPremiumField: false,
      nameField: "",
      emailField: "",
      ageField: 0,
      descriptionField: "",
      customers: [
        {
          id: 1,
          name: "Marciano Daniel Mendes",
          email: "marciano@mendes.com",
          age: 42,
          description:
            "Programador de sistemas na PH Softwares, pai da Júlia e marido da Simone",
          isPremium: false,
        },
        {
          id: 2,
          name: "Julia Mendes",
          email: "julia@mendes.com",
          age: 6,
          description: "Estudante filha de Marciano e Simone",
          isPremium: true,
        },
        {
          id: 3,
          name: "Simone",
          email: "simone@bos.com",
          age: 43,
          description: "Contadora na Unoesc, mãe da Júlia e esposa do Marciano",
          isPremium: true,
        },
      ],
    };
  },
  components: {
    Customer,
    // Product
  },
  methods: {
    registerCustomer: function () {
      if (this.nameField == "") {
        this.occurredError = true;
        return;
      }

      this.customers.push({
        name: this.nameField,
        email: this.emailField,
        age: this.ageField,
        description: this.descriptionField,
        isPremium: this.isPremiumField,
        id: Date.now(),
      });

      this.nameField = "";
      this.emailField = "";
      this.ageField = "";
      this.descriptionField = "";
      this.isPremiumField = false;
      this.occurredError = false;
    },

    deleteCustomer: function ($event) {
      console.log("Recebendo evento!");
      console.log($event.idCustomer);
      var customersFiltereds = this.customers.filter(
        (customer) => customer.id != $event.idCustomer
      );
      this.customers = customersFiltereds;
    },
  },
  computed: {
    orderCustumers: function () {
      return _.orderBy(this.customers, ["name"], ["asc"]);
    },
  },
};
</script>

<style>
#errorName {
  color: red;
}

#sizebox{
  max-width: 600px;;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
