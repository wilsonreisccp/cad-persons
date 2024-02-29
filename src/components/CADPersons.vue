<template>
  <div class="row">
    <div class="col-lg-8 offset-lg-8">
      <div class="table-responsive">
        <DataTable :data="persons" :columns="columns" class="table table-striped table-bordered display" :options="{
          responsive: true, autoWidth: false, dom: 'Btrtip', language: {
            search: 'Buscar',
            zeroRecords: 'Sem registros',
            info: 'Mostrando _START_ a _END_ de _TOTAL_',
            paginate: { fisrt: 'Primeiro', previous: 'Anterior', next: 'Proximo', last: 'Ultimo' }
          }
        }">
          <thead>
            <tr>
              <th>#</th>
              <th>Nome</th>
              <th>email</th>
              <th>Nascimento</th>
            </tr>
          </thead>
        </DataTable>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import DataTable from 'datatables.net-vue3';
import DataTableLib from 'datatables.net-bs5'
import ButtonsHtmlr from 'datatables.net-buttons/js/buttons.html5'
//import pdfmake from 'pdfmake'
//import 'datatables.net-responsive-bs5'

//import JSZip from 'jszip';
//window.JSZip = JSZip;

DataTable.use(DataTableLib)
DataTable.use(ButtonsHtmlr)
//DataTable.use(pdfmake)

export default {
  components: { DataTable },
  data() {
    return {
      persons: null,
      columns: [
        {
          data: null, render: function (data, type, row, meta) { return `${meta.row + 1}` }
        },
        { data: 'name' },
        { data: 'email' },
        { data: 'birthday' }
      ]
    }
  },
  mounted() {
    this.getPersons();
  },
  methods: {
    getPersons() {
      axios.get('https://api-gtr-person.vercel.app/person')
        .then(res => (this.persons = res.data.persons))
    }
  }
}


</script>

<style lang="scss" scoped>
@import 'datatables.net-bs5';
</style>

 