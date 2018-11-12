<template>
  <div id="app">
    <h1 style="text-align:center;">V-EDIT-DIALOG</h1>
    
    <h3> A "Nevek" mező tulajdonságia:</h3><br>
    <ul>
      <li><strong>return-value:</strong> ez állítja be az "Nevek" értékjét.</li>
      <li><strong>lazy</strong></li>
    </ul> 
    <br>
    <h3> A "Sötét téma" mező tulajdonságia:</h3><br>
    <ul>
      <li><strong>return-value:</strong> ez állítja be az "Nevek" értékjét.</li>
      <li><strong>lazy</strong></li>
      <li><strong>large</strong></li>
      <li><strong>dark</strong></li>
      <li><strong>persistent</strong></li>
    </ul> 

    <v-app id="inspire">
      <div>
        <v-data-table
          :headers="headers"
          :items="desserts">
          <template 
            slot="items" 
            slot-scope="props">
            <td>
              <v-edit-dialog
                :return-value.sync="props.item.name"
                lazy
                @save="save"
                @cancel="cancel"
                @open="open"
                @close="close"> {{ props.item.name }}
                <v-text-field
                  slot="input"
                  v-model="props.item.name"
                  :rules="[max25chars]"
                  label="Edit"
                  single-line
                  counter />
              </v-edit-dialog>
            </td>
            <td class="text-xs-right">{{ props.item.mezo_1 }}</td>
            <td class="text-xs-right">{{ props.item.mezo_2 }}</td>
            <td class="text-xs-right">{{ props.item.mezo_3 }}</td>
            <td class="text-xs-right">{{ props.item.mezo_4 }}</td>
            <td class="text-xs-right">
              <v-edit-dialog
                :return-value.sync="props.item.sotet_tema"
                large
                lazy
                dark
                persistent
                @save="save"
                @cancel="cancel"
                @open="open"
                @close="close">
                <div>{{ props.item.sotet_tema }}</div>
                <div 
                  slot="input" 
                  class="mt-3 title">Módosítás</div>
                <v-text-field
                  slot="input"
                  v-model="props.item.sotet_tema"
                  :rules="[max25chars]"
                  label="Edit"
                  single-line
                  counter
                  autofocus />
              </v-edit-dialog>
            </td>
          </template>
        </v-data-table>
    
        <v-snackbar 
          v-model="snack" 
          :timeout="3000" 
          :color="snackColor">
          {{ snackText }}
          <v-btn 
            flat 
            @click="snack = false">Bezárás</v-btn>
        </v-snackbar>
      </div>
    </v-app>

    
  </div>
</template>
<script>
export default {
  data() {
    return {
      snack: false,
      snackColor: "",
      snackText: "",
      max25chars: v => v.length <= 25 || "Túl sok karakter! Maximum 25!",
      pagination: {},
      headers: [
        {
          text: "Nevek",
          align: "left",
          sortable: false,
          value: "name"
        },
        { text: "1. mező", value: "mezo_1" },
        { text: "2. mező", value: "mezo_2" },
        { text: "3. mező", value: "mezo_3" },
        { text: "4. mező ", value: "mezo_4" },
        { text: "Sötét téma", value: "sotet_tema" }
      ],
      desserts: [
        {
          value: false,
          name: "Teszt Elek",
          mezo_1: 159,
          mezo_2: 6.0,
          mezo_3: 24,
          mezo_4: 4.0,
          sotet_tema: "Túl sötét!"
        },
        {
          value: false,
          name: "Gipsz Jakab",
          mezo_1: 237,
          mezo_2: 9.0,
          mezo_3: 37,
          mezo_4: 4.3,
          sotet_tema: "Túl sötét!"
        },
        {
          value: false,
          name: "Jakab József",
          mezo_1: 262,
          mezo_2: 16.0,
          mezo_3: 23,
          mezo_4: 6.0,
          sotet_tema: "Túl sötét!"
        },
        {
          value: false,
          name: "Példa Áron",
          mezo_1: 305,
          mezo_2: 3.7,
          mezo_3: 67,
          mezo_4: 4.3,
          sotet_tema: "Túl sötét!"
        },
        {
          value: false,
          name: "John Wick",
          mezo_1: 356,
          mezo_2: 16.0,
          mezo_3: 49,
          mezo_4: 3.9,
          sotet_tema: "Túl sötét!"
        }
      ]
    };
  },
  methods: {
    save() {
      this.snack = true;
      this.snackColor = "success";
      this.snackText = "Mentve";
    },
    cancel() {
      this.snack = true;
      this.snackColor = "error";
      this.snackText = "Megszakítva";
    },
    open() {
      this.snack = true;
      this.snackColor = "info";
      this.snackText = "Megnyitva";
    },
    close() {}
  }
};
</script>
