<template>
  <q-page class="flex page">
    <div class="row justify-between light headerBar">
      <div class="overview text">Overview</div>
      <q-dialog v-model="searchbar" :position="searchbarPos">
        <div class="fluent">
          <q-input
            bottom-slots
            v-model="inputTextSearch"
            style="width:500px"
            :dense="true"
            clearable
            standout
            bg-color="indigo-5"
            autofocus
          >
            <template v-slot:prepend>
              <q-icon name="las la-search" />
            </template>
          </q-input>
          <div>
            <q-scroll-area style="height: 200px;">
              <div v-for="n in 50" :key="n">
                <q-item clickable
                  ><q-icon
                    name="las la-search"
                    size="20px"
                    color="grey-8"
                    style="padding-right: 10px"
                  />
                  <p style="color:grey">Result N°{{ n }}</p>
                </q-item>
              </div>
            </q-scroll-area>
          </div>
        </div>
      </q-dialog>
      <div class="row" style="position:absolute;right:2%;margin-left:200px;">
        <div>
          <q-btn
            color="grey"
            icon="las la-search"
            flat
            round
            @click="searchbar = true"
          />
        </div>
        <div>
          <q-btn color="grey" icon="las la-bell" flat round
            ><q-badge floating color="red" transparent rounded
              >+5</q-badge
            ></q-btn
          >
          <q-popup-edit
             value=""
            :cover="false"
            style="background:transparent;margin:0px;padding:0px"
          >
            <div style="height: 200px; width:150px; margin:0px">
              <q-scroll-area style="height: 200px; width:100% ; margin:0px">
                <q-item
                  clickable
                  v-for="i in 10"
                  :key="i"
                  style="border-radius:10px;"
                  >Message {{ i }}</q-item
                >
              </q-scroll-area>
            </div>
          </q-popup-edit>
        </div>
        <q-separator vertical style="margin:10px" />
        <div class="row" style="margin:2px">
          <p style="padding: 10px 10px 0px 5px" class="text">{{ username }}</p>

          <q-avatar size="40px">
            <img src="~/assets/avatar.png" alt="" />
          </q-avatar>
        </div>
      </div>
    </div>

    <div
      class="row"
      style="width: 100%;
               height: 100%;
               display: flex;
               "
    >
      <div style="flex:0.7;">
        <div class=" widget fluent" onclick="()';" style="cursor: pointer; ">
          <iframe
            src="https://free.timeanddate.com/clock/i7untxj0/n253/fn16/fs30/tct/pct/pa9/tt0/tw0/tm1/td2/th1/tb4"
            frameborder="0"
            width="100%"
            height="88"
            allowtransparency="true"
          ></iframe>
        </div>
        <div
          class="widget fluent"
          onclick="()';"
          style="cursor: pointer;  width:90% ;height:65%"
        >
          <q-btn
            color="white"
            icon="las la-music"
            @click="yt = !yt"
            size="50px"
            style="width:100px;height:100px;position:relative;top:30%;left:30%;z-index:1"
            flat
            rounded
            dense
          />
          <q-video
            v-show="yt"
            class="absolute-full"
            src="https://www.youtube.com/embed/ylfDBdEXrBQ"
          />
        </div>
      </div>

      <div
        class="widget fluent"
        style="cursor: pointer; height:400px ;min-width:400px;flex:2;"
      >
        <vue-highcharts
          :options="areaOptions"
          ref="areaCharts"
        ></vue-highcharts>
      </div>

      <div
        class="widget fluent"
        onclick="()';"
        style="cursor: pointer; height:400px ; flex:0.5 ;"
      ></div>
      <div class="widget fluent" style="padding:10px;width:100%;">
        <q-table
          title="Test"
          :columns="columns"
          row-key="name"
          selection="single"
          :selected.sync="selected"
          color="#e4e4e4d2"
          card-class="#e4e4e4d2"
          table-class="text-grey-8"
          table-header-class="text-black"
          style="width:100%"
          :data="DataTable.data"
          :loading="loading"
          :filter="filter"
          @request="onRequest"
          binary-state-sort
        >
          <template v-slot:top-right>
            <q-input
              borderless
              dense
              debounce="300"
              v-model="filter"
              placeholder="Search"
            >
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>
          </template>
        </q-table>
         <q-menu touch-position context-menu>
      <q-list dense style="min-width: 100px ; margin:10px 0px 5px 0px">
        <q-item clickable v-close-popup>
          <div class="row">
            <q-icon
              name="las la-external-link-alt"
              size="xs"
              style="padding-right:10px"
            />Open
          </div>
        </q-item>
        <q-item clickable v-close-popup>
          <q-item-section @click="CopyData(JSON.stringify(selected))">
            <div class="row">
              <q-icon
                name="las la-copy"
                size="sm"
                style="padding-right:5px"
              />Copy
            </div>
          </q-item-section>
        </q-item>
        <q-separator />
        <q-item clickable>
          <q-item-section @click="exportTable" no-caps
            ><div class="row">
              <q-icon
                name="las la-file-export"
                size="sm"
                style="padding-right:5px"
              />Export
            </div></q-item-section
          >
        </q-item>
        <q-separator />
      </q-list>
    </q-menu>
      </div>
    </div>
    <q-dialog v-model="calc" :position="positionCalc" seamless>
      <q-card style="padding:20px;border-radius:20px;">
        <q-btn color="black" icon="close" v-close-popup round flat />

        <table border="0">
          <tr>
            <td colspan="3">
              <q-input
                type="text"
                id="result"
                rounded
                dense
                v-model="text"
                autogrow
              />
            </td>
            <!-- clr() function will call clr to clear all label -->
            <td><q-btn label="C" @click="clr()" color="orange" round /></td>
          </tr>
          <tr>
            <!-- create button and assign label to each button -->
            <!-- dis("1") will call function dis to display label -->
            <td><q-btn label="1" round @click="dis('1')" /></td>
            <td><q-btn label="2" round @click="dis('2')" /></td>
            <td><q-btn label="3" round @click="dis('3')" /></td>
            <td><q-btn label="/" round @click="dis('/')" color="black" /></td>
          </tr>
          <tr>
            <td><q-btn label="4" round @click="dis('4')" /></td>
            <td><q-btn label="5" round @click="dis('5')" /></td>
            <td><q-btn label="6" round @click="dis('6')" /></td>
            <td><q-btn label="-" round @click="dis('-')" color="black" /></td>
          </tr>
          <tr>
            <td><q-btn label="7" round @click="dis('7')" /></td>
            <td><q-btn label="8" round @click="dis('8')" /></td>
            <td><q-btn label="9" round @click="dis('9')" /></td>
            <td><q-btn label="+" round @click="dis('+')" color="black" /></td>
          </tr>
          <tr>
            <td><q-btn label="." round @click="dis('.')" /></td>
            <td><q-btn label="0" round @click="dis('0')" /></td>
            <!-- solve function call function solve to evaluate label -->
            <td><q-btn label="=" @click="solve()" round color="indigo-8" /></td>
            <td>
              <q-btn label="x" round @click="dis('*')" color="black" />
            </td>
          </tr>
        </table>
      </q-card>
    </q-dialog>
    <q-page-sticky position="bottom-right" :offset="fabPos">
      <q-btn
        fab
        icon="las la-calculator"
        color="brand"
        @click="calc = true"
        :disable="draggingFab"
        v-touch-pan.prevent.mouse="moveFab"
      />
    </q-page-sticky>
    <!-- Context Menu  -->
   
  </q-page>
</template>

<script>
import VueHighcharts from "vue2-highcharts";
import * as data from "src/assets/Data.js";
import json from "src/assets/DataTable.json";
import { copyToClipboard } from "quasar";
import { exportFile } from "quasar";

function wrapCsvValue(val, formatFn) {
  let formatted = formatFn !== void 0 ? formatFn(val) : val;

  formatted =
    formatted === void 0 || formatted === null ? "" : String(formatted);

  formatted = formatted
    .split('"')
    .join('""')
    /**
     * Excel accepts \n and \r in strings, but some other CSV parsers do not
     * Uncomment the next two lines to escape new lines
     */
    .split("\n")
    .join("\\n")
    .split("\r")
    .join("\\r");

  return `"${formatted}"`;
}
export default {
  name: "Home",
  components: {
    VueHighcharts
  },
  data() {
    return {
      text: "",
      fabPos: [18, 18],
      draggingFab: false,
      filter: "",
      loading: false,
      positionCalc: "right",
      calc: false,
      yt: false,
      inputTextSearch: "",
      DataTable: json,
      username: "Roboto Dakasuki Mora",
      searchbar: false,
      searchbarPos: "top",
      areaOptions: data.AreaData,
      selected: [],
      columns: [
        {
          name: "desc",
          required: true,
          label: "Dessert (100g serving)",
          align: "left",
          field: row => row.name,
          format: val => `${val}`,
          sortable: true
        },
        {
          name: "calories",
          align: "center",
          label: "Calories",
          field: "calories",
          sortable: true
        },
        { name: "fat", label: "Fat (g)", field: "fat", sortable: true },
        { name: "carbs", label: "Carbs (g)", field: "carbs" },
        { name: "protein", label: "Protein (g)", field: "protein" },
        { name: "sodium", label: "Sodium (mg)", field: "sodium" },
        {
          name: "calcium",
          label: "Calcium (%)",
          field: "calcium",
          sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        },
        {
          name: "iron",
          label: "Iron (%)",
          field: "iron",
          sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        }
      ]
    };
  },

  mounted() {
    this.onRequest({
      filter: undefined
    });
  },
  methods: {
    
    clr() {
      this.text = "";
    },
    solve() {
      this.text = eval(this.text) ;
    },
    dis(d) {
      this.text = this.text.concat(d);
    },
    moveFab(ev) {
      this.draggingFab = ev.isFirst !== true && ev.isFinal !== true;

      this.fabPos = [this.fabPos[0] - ev.delta.x, this.fabPos[1] - ev.delta.y];
    },
    exportTable() {
      // naive encoding to csv format
      const content = [this.columns.map(col => wrapCsvValue(col.label))]
        .concat(
          this.data.map(row =>
            this.columns
              .map(col =>
                wrapCsvValue(
                  typeof col.field === "function"
                    ? col.field(row)
                    : row[col.field === void 0 ? col.name : col.field],
                  col.format
                )
              )
              .join(",")
          )
        )
        .join("\r\n");

      const status = exportFile("table-export.csv", content, "text/csv");

      if (status !== true) {
        this.$q.notify({
          message: "Browser denied file download...",
          color: "negative",
          icon: "warning"
        });
      }
    },
    showNotif(position) {
      setTimeout(() => {
        this.$q.notify({
          message: "Hello World!",
          color: "blue",
          position,
          progress: true
        });
      }, 50);
    },
    CopyData(CopyTab) {
      let CSVData = "";
      // set the column names
      for (const value of Object.keys(CopyTab[0][0])) {
        CSVData = CSVData.concat(value + ",");
      }
      CSVData = CSVData.slice(0, CSVData.length - 1);
      CSVData = CSVData.concat("\n");

      // parse the data
      for (const tbl of CopyTab) {
        for (const row of tbl) {
          for (const value of Object.values(row)) {
            CSVData = CSVData.concat(value + ",");
          }
          CSVData = CSVData.slice(0, CSVData.length - 2);
          CSVData = CSVData.concat("\n");
        }
      }
      copyToClipboard(CopyTab)
        .then(() => {
          // success!
        })
        .catch(() => {
          // fail
        });
      document.getElementById("csvdata").innerText = CSVData;
    },
    onRequest(props) {
      const { page, rowsPerPage, sortBy, descending } = props.pagination;
      const filter = props.filter;

      this.loading = true;

      // emulate server
      setTimeout(() => {
        // update rowsCount with appropriate value
        this.pagination.rowsNumber = this.getRowsNumberCount(filter);

        // get all rows if "All" (0) is selected
        const fetchCount =
          rowsPerPage === 0 ? this.pagination.rowsNumber : rowsPerPage;

        // calculate starting row of data
        const startRow = (page - 1) * rowsPerPage;

        // fetch data from "server"
        const returnedData = this.fetchFromServer(
          startRow,
          fetchCount,
          filter,
          sortBy,
          descending
        );

        // clear out existing data and add new
        this.data.splice(0, this.data.length, ...returnedData);

        // don't forget to update local pagination object
        this.pagination.page = page;
        this.pagination.rowsPerPage = rowsPerPage;
        this.pagination.sortBy = sortBy;
        this.pagination.descending = descending;

        // ...and turn of loading indicator
        this.loading = false;
      }, 1500);
    },

    // emulate ajax call
    // SELECT * FROM ... WHERE...LIMIT...
    fetchFromServer(startRow, count, filter, sortBy, descending) {
      const data = filter
        ? this.original.filter(row => row.name.includes(filter))
        : this.original.slice();

      // handle sortBy
      if (sortBy) {
        const sortFn =
          sortBy === "desc"
            ? descending
              ? (a, b) => (a.name > b.name ? -1 : a.name < b.name ? 1 : 0)
              : (a, b) => (a.name > b.name ? 1 : a.name < b.name ? -1 : 0)
            : descending
            ? (a, b) => parseFloat(b[sortBy]) - parseFloat(a[sortBy])
            : (a, b) => parseFloat(a[sortBy]) - parseFloat(b[sortBy]);
        data.sort(sortFn);
      }

      return data.slice(startRow, startRow + count);
    },

    // emulate 'SELECT count(*) FROM ...WHERE...'
    getRowsNumberCount(filter) {
      if (!filter) {
        return this.original.length;
      }
      let count = 0;
      this.original.forEach(treat => {
        if (treat.name.includes(filter)) {
          ++count;
        }
      });
      return count;
    }
  },
  components: {
    VueHighcharts
  }
};
</script>
