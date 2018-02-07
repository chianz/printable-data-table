# printable-data-table

A Vue component that shows data table which can be printed. It is a wrapper of `vue2-datatable-component` (https://github.com/OneWayTech/vue2-datatable) module.

npm package url: https://www.npmjs.com/package/printable-data-table

This isn't particularly useful, it's used as a demo for how to publish Vue components to NPM!

## Publish to npm
```js
npm publish
```

## Dependencies

`bootstrap`

## Installation

```js
npm i --save-dev printable-data-table
```

### Module

```js
import Vue from 'vue'
import PrintableDataTable from 'printable-data-table'

Vue.component('printable-data-table', PrintableDaTable)
```

## Usage

Once installed, it can be used in a template as:

```html
<printable-data-table v-bind="$data"></printable-data-table>
```

where you define data as below:

```js
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
      data: [
        { name: 'Orange', price: 4.80, desc: 'Chinese Orange' },
        { name: 'Apple', price: 5.50, desc: 'American Apple' },
        { name: 'Pear', price: 4.50, desc: 'Malaysian Pear' },
        { name: 'Dragonfruit', price: 2.80, desc: 'Vietnamese Red Dragonfruit' },
        { name: 'Watermelon', price: 5.70, desc: 'Taiwanese Watermelon' },
        { name: 'Grape', price: 7.20, desc: 'Chilean Grapes' }
      ],
      total: 6,
      query: { 'limit': 10, 'offset': 0, 'sort': '', 'order': '' },
    }
  }
  ```

