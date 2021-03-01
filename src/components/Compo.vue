<template>
  <v-container fluid fill-height>
    <v-layout fill-height>
      <v-flex flexbox>

        <v-data-table :headers="headers" :items="objects" class="elevation-1" sort-by="name" fixed-header>
          <template v-slot:top>
            <v-toolbar flat color="white">
              <v-toolbar-title>OBJECTS</v-toolbar-title>
              <v-spacer></v-spacer>
            </v-toolbar>
          </template>

          <template v-slot:item="{ item }">
            <tr v-on:dblclick="editObject(item)">
              <td><v-layout justify-center>{{ item.id }}</v-layout></td>
              <td><v-layout justify-center>{{ item.name }}</v-layout></td>
              <td>
                <v-layout justify-center>
                  <v-chip v-for="group in item.groups" :key="group.id" class="ma-2"> {{ group.name }}</v-chip>
                </v-layout>
              </td>
              <td>
                <v-layout justify-center>

                  <v-tooltip bottom>
                    <template v-slot:activator="{ on }">
                      <v-icon small class="mr-2" v-on="on" @click="editObject(item)">edit</v-icon>
                    </template>
                    <span>Modify</span>
                  </v-tooltip>

                </v-layout>
              </td>
            </tr>
          </template>
        </v-data-table>
      </v-flex>

      
      <v-dialog v-model="showEditDialog" max-width="900px" @keydown.esc="showDeleteDialog = false" @keydown.enter="confirmEditDialog">
        
        <v-card>
          <v-card-title>
            <span class="headline">Dialog</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12" xs="12" sm="12" md="12">
                  <v-text-field v-model="editingObject.name" class="mt-3"></v-text-field>
                </v-col>
              </v-row>
              <v-row>
                <v-col cols="12" xs="12" sm="12" md="12">
                  <v-autocomplete
                    v-model="editingObject.managed_by"
                    :items="groups"
                    item-text="name"
                    item-value="id"
                    multiple
                    chips
                    deletable-chips
                  ></v-autocomplete>
                </v-col> 
              </v-row>

            </v-container>
          </v-card-text>
          <v-card-actions>
            <div class="flex-grow-1"></div>
            <v-btn @click="showEditDialog=false">Annuler</v-btn>
            <v-btn color="primary" @click="showEditDialog=false">Enregistrer</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>


    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'Compo',
  data: () => ({
    headers: [{ text: 'ID', align: 'center', value: 'id', filterable: true },
              { text: 'Name', align: 'center', value: 'name', filterable: false },
              { text: 'Groups', align: 'center', value: 'groups', filterable: false },
              { text: 'Actions', align: 'center', value: 'actions', filterable: false }
              
              ],
    objects : [{"id": 1, "name": "AAA", groups: [{"id":1, "name": "G1"}, {"id":2, "name": "G2"}]},
               {"id": 2, "name": "BBB", groups: [{"id":3, "name": "G3"}, {"id":4, "name": "G4"}]},
               {"id": 3, "name": "CCC", groups: [{"id":5, "name": "G5"}, {"id":6, "name": "G6"}]}],
    groups: [{"id":1, "name": "G1"}, {"id":2, "name": "G2"}, {"id":3, "name": "G3"}, {"id":4, "name": "G4"}, {"id":5, "name": "G5"}, {"id":6, "name": "G6"}],
    showEditDialog: false,
    editingObject: {"groups": []}
  }),
  methods: {
    editObject (obj) {
      console.log("editObject")
      this.editingObject = Object.assign({}, obj)
      this.editing = true
      this.showEditDialog = true
    },
  }
}
</script>


<style scoped>

</style>
