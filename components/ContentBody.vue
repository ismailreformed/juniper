<template>
  <div>
    <b-card>
      <b-form-group label="Filter by Build State:" label-cols-md="4">
        <b-form-select v-model="filter" :options="buildStateOptions" class="mb-3" />
      </b-form-group>
      <b-form-group label="Filter by Build Name:" label-cols-md="4">
        <b-form-select v-model="filter" :options="buildNameOptions" class="mb-3" />
      </b-form-group>

      <hr>
      <b-form-group label="Selection mode:" label-cols-md="4">
        <b-form-select v-model="selectMode" :options="modes" />
      </b-form-group>
      <b-table
        ref="selectableTable"
        selectable
        bordered
        outlined
        fixed
        :select-mode="selectMode"
        :items="items"
        :fields="fields"
        responsive="sm"
        head-variant="light"
        :filter="filter"
        @row-selected="onRowSelected"
      >
        <!-- Example scoped slot for select state illustrative purposes -->
        <template v-slot:cell(compare)="{ rowSelected }">
          <template v-if="rowSelected">
            <span aria-hidden="true">&check;</span>
            <span class="sr-only">Selected</span>
          </template>
          <template v-else>
            <span aria-hidden="true">&nbsp;</span>
            <span class="sr-only">Not selected</span>
          </template>
        </template>
      </b-table>
      <p>
        <b-button size="sm" @click="selectAllRows">
          Select all
        </b-button>
        <b-button size="sm" @click="clearSelected">
          Clear selected
        </b-button>
      </p>
    </b-card>

    <!-- /* Example of getting data from api */ -->
    <br>
    <b-card
      title="Bitcoin List, Get Api data by axios Example"
    >
      <b-table
        ref="selectableTable"

        selectable
        bordered
        outlined
        fixed
        select-mode="multi"
        :items="info"
        :fields="infoFields"
        responsive="sm"
        head-variant="light"
        :filter="filter"
        @row-selected="onRowSelected"
      >
        <!-- Example scoped slot for select state illustrative purposes -->
        <template v-slot:cell(selected)="{ rowSelected }">
          <template v-if="rowSelected">
            <span aria-hidden="true">&check;</span>
            <span class="sr-only">Selected</span>
          </template>
          <template v-else>
            <span aria-hidden="true">&nbsp;</span>
            <span class="sr-only">Not selected</span>
          </template>
        </template>
      </b-table>
      <p>
        <b-button size="sm" @click="selectAllRows">
          Select all
        </b-button>
        <b-button size="sm" @click="clearSelected">
          Clear selected
        </b-button>
      </p>
    </b-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      modes: ['multi', 'single', 'range'],

      fields: [
        {
          key: 'compare',
          sortable: false
        },
        {
          key: 'build_name',
          sortable: true
        },
        {
          key: 'build_state',
          sortable: true
        },
        {
          key: 'build_path',
          sortable: true
        },
        {
          key: 'action',
          sortable: false
        }
      ],

      items: [
        { build_name: '17.2R1.5', build_state: 'Skipped', build_path: '/volume/build/junos/17.2/release/17.2R1.5' },
        { build_name: '17.2R1.6', build_state: 'Deleted', build_path: '/volume/build/junos/17.2/release/17.2R1.5' },
        { build_name: '17.2R1.7', build_state: 'Activated', build_path: '/volume/build/junos/17.2/release/17.2R1.5' }
      ],
      selectMode: 'multi',
      compare: [],
      filter: '',
      buildStateOptions: [
        { value: '', text: 'None' },
        { value: 'Skipped', text: 'Skipped' },
        { value: 'Deleted', text: 'Deleted' },
        { value: 'Activated', text: 'Activated' }
      ],
      buildNameOptions: [
        { value: '', text: 'None' },
        { value: '17.2R1.5', text: '17.2R1.5' },
        { value: '17.2R1.6', text: '17.2R1.6' },
        { value: '17.2R1.7', text: '17.2R1.7' }
      ],
      infoFields: [
        {
          key: 'selected',
          sortable: false
        },
        {
          key: 'code',
          sortable: true
        },
        {
          key: 'description',
          sortable: true
        },
        {
          key: 'rate',
          sortable: true
        },
        {
          key: 'rate_float',
          sortable: false
        },
        {
          key: 'symbol',
          sortable: false
        }
      ],
      info: []

    }
  },

  /* An example of calling api after created the component by axios */
  mounted () {
    this.$axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then((response) => {
        const data = response.data.bpi
        const result = Object.keys(data).map(function (key) {
          return [Number(key), data[key]][1]
        })
        this.info = result
      })
  },

  methods: {
    onRowSelected (items) {
      this.compare = items
    },
    selectAllRows () {
      this.$refs.selectableTable.selectAllRows()
    },
    clearSelected () {
      this.$refs.selectableTable.clearSelected()
    },
    selectThirdRow () {
      // Rows are indexed from 0, so the third row is index 2
      this.$refs.selectableTable.selectRow(2)
    },
    unselectThirdRow () {
      // Rows are indexed from 0, so the third row is index 2
      this.$refs.selectableTable.unselectRow(2)
    }
  }
}
</script>
