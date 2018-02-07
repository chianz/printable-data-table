<template>
<div id="product-table">
  <div class="panel panel-default">
      <div class="panel-heading" data-toggle="collapse" href="#collapse_body">Search</div>
      <div id="collapse_body" class="panel-body panel-collapse collapse">
        <div class="row form-group">
          <div class="col-xs-12 col-sm-2"><label for="name">Name:</label></div>
          <div class="col-xs-12 col-sm-5">
            <input id="name" class="form-control" type="text" v-model="search.name"/>
          </div>
        </div>
        <div class="row form-group">
          <div class="col-xs-12 col-sm-2"><label for="description">Description:</label></div>
          <div class="col-xs-12 col-sm-5">
            <input id="customer" class="form-control" type="text" v-model="search.description"/>
          </div>
        </div>
        <div class="row form-group">
          <div class="col-xs-12">
            <button class="btn btn-default pull-left" @click="updateData">Search</button>
            <button class="btn btn-default pull-left" @click="viewAll">View All</button>
          </div>
        </div>
      </div>
    </div>

  <printable-datatable v-bind="$data"></printable-datatable>
</div>
</template>
<script>
import Vue from 'vue'
import PrintableDataTable from 'printable-data-table'
import _ from 'lodash'

Vue.component('printable-datatable', PrintableDataTable)

export default {
  name: 'ProductTable',
  data () {
    return {
      tblClass: 'table-bordered',
      pageSizeOptions: [5, 10, 15, 20, 25],
      selection: [],
      columns: [
        { title: 'Name', field: 'name', sortable: true },
        { title: 'Price per kg ($)', field: 'price', sortable: true },
        { title: 'Description', field: 'desc', sortable: true }
      ],
      data: [],
      total: 6,
      query: { 'limit': 10, 'offset': 0, 'sort': '', 'order': '' },
      allData: [
        { name: 'Orange', price: 4.80, desc: 'Chinese Orange' },
        { name: 'Apple', price: 5.50, desc: 'American Apple' },
        { name: 'Pear', price: 4.50, desc: 'Malaysian Pear' },
        { name: 'Dragonfruit', price: 2.80, desc: 'Vietnamese Red Dragonfruit' },
        { name: 'Watermelon', price: 5.70, desc: 'Taiwanese Watermelon' },
        { name: 'Grape', price: 7.20, desc: 'Chilean Grapes' }
      ],
      search: {
        name: '',
        description: ''
      }
    }
  },
  methods: {
    updateData: function () {
      let name = this.search.name
      let description = this.search.description

      this.data = _.filter(this.allData, function (o) {
        return (o.name.toLowerCase().indexOf(name.toLowerCase()) > -1 &&
        o.desc.toLowerCase().indexOf(description.toLowerCase()) > -1)
      })
    },
    viewAll: function () {
      Object.assign(this.search, {name: '', description: ''})
      this.updateData()
    }
  },
  watch: {
    query: {
      handler (query) {
        this.data = _.orderBy(this.allData, [query.sort], [query.order]).slice(query.offset, query.offset + query.limit)
      },
      deep: true
    }
  },
  mounted () {
    this.updateData()
  }
}

</script>
<style scoped>
#product-table {
  padding: 0px 18px;
}

#product-table .panel {
  width: 50%;
}
</style>
