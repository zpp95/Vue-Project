<template>
  <div id="app">
    <h2>Employee Directory</h2>
    <TableView
      :headers="columns"
      :rows="userInfo"
      :sort="sort1"
    >
      <template v-slot:items="{ row }">
        <td>{{ row.name }}</td>
        <td>{{ row.id }}</td>   
        <td>{{ row.email }}</td>              
        <td>{{ row.gender }}</td>     
        <td>{{ row.status }}</td>     
      </template>

      <template v-slot:no-data>
        <span>No data</span>
      </template>
    </TableView>
  </div>
</template>

<script>
import axios from 'axios'
import TableView from './TableView.vue'
import { columns } from '@/data'

export default {
  name: 'HelloWorld',
  components: {
    TableView,
  },
  props: {
    msg: String
  },
   data() {
    return {
      columns: columns,
      userInfo: [], 
      sort1:{
        field: 'name',
        order: 'asc'
      },    
      pagination:{
        itemsPerPage: 7,
        align: 'center',
        visualStyle: 'select'
      },
    };
  },

    methods: {
    async fetctUserFacts() {
    const infoResponse = await axios.get(
      "https://gorest.co.in/public/v2/users"
    );
    this.userInfo = infoResponse.data;
    console.log("data", infoResponse.data);
  },
    },
    async mounted() {
      await this.fetctUserFacts();
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import url(https://fonts.googleapis.com/css?family=Roboto+Mono);

body, html{
  height: 100%;
}
#app {
  font-family: 'Roboto Mono', Helvetica, Arial, sans-serif;
  font-size: 15px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 100%;
  margin: 0 auto;
}
h1{
  margin-bottom: 2em;
  color: #f90;
}
.separator{
  margin: 2em 0;
  text-align: center;
}
.custom-style {
  // Table styles
  .ozn-table {
    border-collapse: collapse;
    width: 100%;
    thead {
      th { 
        border-bottom: 1px solid #ffffff;
        padding: 0 10px;
        height: 48px;
        text-align: left; 
        font-size: 1em; 
        color: #fff;
        background-color: #7cc3fd; 
        cursor: pointer; 
        &:hover{
          span{
            text-decoration: underline;
            text-decoration-style: dotted;
          }
        }        
        i{
          color: #ffffff; 
          &.active{
            color: #ff00aa;
            + span{
              color: #a9237c;
            }
          }
        }       
      }
    }
    tbody {
      tr{
        &:nth-child(odd){
          background-color: #e9f5ff;
        }
        &:nth-child(even){
          background-color: #fafaeb;
        }
      }
      td {
        border-bottom: 1px solid #ffffff;
        padding: 0 10px;
        height: 48px;
        font-size: 1em; 
      }
    }
  }
  // Paginator styles    
  .ozn-paginator{
    margin-top: .5em;
    select{
      border: 1px solid #7cc3fd;
      border-radius: 8px;
      color: #ffffff;
      background-color:  #7cc3fd;
      outline: none;
    }
    button{
      border: 1px solid #7cc3fd;
      border-radius: 8px;
      color: #ffffff;
      background-color:  #7cc3fd;
      outline: none;
    }    
  }

}
</style>
