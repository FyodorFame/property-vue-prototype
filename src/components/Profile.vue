<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>      
    </v-row>

    <v-data-table
        :headers="headers"
        :items="items"
        class="elevation-1"
    >
    
        <template v-slot:item.title="props">
            <v-edit-dialog 
                :return-value.sync="props.item.title"
                @open="open"
                > {{ props.item.title }}
                <template v-slot:input>
                    <v-text-field 
                        v-model="props.item.title"
                        :rules="[max25chars]"
                        :label="Edit"    
                    ></v-text-field>
                </template>
            </v-edit-dialog>
        </template>

    </v-data-table>
  </v-container>
</template>

<script>
    export default {
        data: () => ({
            snack: false,
            snackColour: '',
            snackText: '',
            max25chars: v => v.length <= 25 || 'Invalid',
            headers: [
                {
                    text: 'Name',
                    value: 'title'
                }
            ],
            items: [
                {
                    id: 1,
                    title: '34 Walnut Grove'
                },
                {
                    id: 2,
                    title: '87 Wellington St'
                },
                {
                    id: 3,
                    title:'876 Queen Street'
                },
                {
                    id: 4,
                    title: '234 North Street'
                }
            ]
        }),
        methods: {
            open() {
                this.snack = true,
                this.snackColour = 'info',
                this.snackText = 'Dialog opened'
            }
        }
    }
</script>