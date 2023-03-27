<template>
   <ag-grid-vue
    style="width: 500px; height: 200px"
    class="ag-theme-alpine"
    :columnDefs="columnDefs"
    :rowData="rowData"
  >
  </ag-grid-vue>
  
</template>

<script>
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
import { AgGridVue } from "ag-grid-vue3";

    export default {
        name: 'App',
        data() {
            return {
                columnDefs: null,
                rowData: null,
                gridOptions: null,
                ticketData: [],
              
              }
        },
        components: {
            AgGridVue
        },

        beforeMount() {
            this.columnDefs = [
                { field: 'id' },
                { field: 'title' },
                { field: 'userId' },
                { field: 'completed'}
            ];
            this.$axios
       .get('https://jsonplaceholder.typicode.com/todos/3')
       .then((res) => {
       //  alert("id=>" + res.data["id"] );
       this.rowData = [res.data];
        // this.rowData = this.ticketData;
        // var aaa = JSON.parse(JSON.stringify(res.data))
        //  this.kkk = res.data["id"];
        //  this.title = res.data["title"];
        //  alert("id=>" + res.data["id"] );
        //  console.log(res.staus);
          console.log(res.data);
        //  this.rowData = [
        //         { id: res.data["id"] , title: 'Celica', userId: 35000 },
        //          { id: 'Ford', title: 'Mondeo', userId: 32000 },
        //          { id: 'Porsche', title: 'Boxter', userId: 72000 }
        //     ]
       })
       .catch((error) => {
         console.log(error);
       })
       .finally(() => {
         console.log("항상 마지막에 실행");
       });
    //    this.gridOptions = {}
    // this.gridOptions.rowData = this.ticketData
    // this.ticketData = response.data
     // this is not working
            // this.rowData = [
            //     { make: 'Toyota', model: 'Celica', price: 35000 },
            //     { make: 'Ford', model: 'Mondeo', price: 32000 },
            //     { make: 'Porsche', model: 'Boxter', price: 72000 }
            // ];
        }
    }
</script>