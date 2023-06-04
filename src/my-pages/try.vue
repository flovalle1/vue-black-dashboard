<template>
    <div class="page">
        <card>
          <span slot="header">
            Verwalte deine wöchentliche Anzahl an Leads
          </span>
          <h4 class="card-title">Aktuelle Anzahl Leads: {{ inputValue }}</h4>
          <h4 class="card-title">Wöchentlich möglich: {{ inputValue }}</h4>
          <base-input
            label="Leads"
            v-model.number="inputValue"
            placeholder="Gib hier deine gewünschte wöchentliche Leadanzahl an."
          >
          </base-input>
          <base-button @click="handle_input">Absenden</base-button>
        </card>
    </div>
  </template>
  
  <script>
  export default {
    name: "empty-template",

    data() {
    return {
      inputValue: null,
    }
    },

    methods: {
        handle_input() {
            if (!isNaN(this.inputValue)) {
                this.$notify({ type: 'success', message: `Anzahl aktualisiert auf ${this.inputValue}` });
            } else {
                this.$notify({ type: 'danger', message: `Fehler! Bitte gib eine gültige Zahl an.` });
            }
        },

        async fetchData() {
          // Datenbankabfrage durchführen (z.B. über einen API-Aufruf)
         try {
           const response = await fetch('http://numbersapi.com/random');
           const data = await response.text();

           this.inputValue = data;
         } catch (error) {
           console.error(error);
         }
        }
        }
  };
 


  </script>
  
  <style>
  .page {
    /* CSS-Stile für deine eigene Seite */
  }
  </style>
