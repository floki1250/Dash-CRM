<template>
  <q-page class="flex page">
    <div class="row justify-between light headerBar">
      <div class="overview text">Overview</div>

      <div class="row" style="position:absolute;right:2%;margin-left:200px;">
        <div>
          <q-btn color="grey" :icon="modeicon" flat round @click="Darkmode" />
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
          <p style="padding: 10px 10px 0px 5px" class="text">
            {{ username }}
          </p>

          <q-avatar size="40px">
            <img src="../assets/avatar.png" alt="" />
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
          <q-carousel
            v-model="slide"
            transition-prev="jump-right"
            transition-next="jump-left"
            swipeable
            animated
            control-color="grey-8"
            control-type="flat"
            prev-icon="arrow_left"
            next-icon="arrow_right"
            navigation-icon="radio_button_unchecked"
            navigation
            padding
            arrows
            height="100%"
            width="100%"
            class="bg-transparent text-black rounded-borders"
          >
            <q-carousel-slide
              name="las la-chart-area"
              class="column no-wrap flex-center"
            >
              <q-icon size="56px"
                ><img src="../assets/growth.svg" alt=""
              /></q-icon>
              <div class="q-mt-md text-center">
                Revenue Increased By 5% this Month
              </div>
            </q-carousel-slide>
            <q-carousel-slide
              name="las la-chart-bar"
              class="column no-wrap flex-center"
            >
              <q-icon size="56px"
                ><img src="../assets/decrease.svg" alt=""
              /></q-icon>
              <div class="q-mt-md text-center">
                Lost 500$ this Week
              </div>
            </q-carousel-slide>
            <q-carousel-slide
              name="las la-project-diagram"
              class="column no-wrap flex-center"
            >
              <q-icon size="56px"
                ><img src="../assets/bank.svg" alt=""
              /></q-icon>
              <div class="q-mt-md text-center">
                Added 1000$ To the Bank
              </div>
            </q-carousel-slide>
            <q-carousel-slide
              name="las la-chart-line"
              class="column no-wrap flex-center"
            >
              <q-icon size="56px"
                ><img src="../assets/balance.svg" alt=""
              /></q-icon>
              <div class="q-mt-md text-center">
                Your Balance 20,000,000 $
              </div>
            </q-carousel-slide>
          </q-carousel>
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
          table-class="text-black-8"
          table-header-class="text-black"
          style="width:100%"
          :data="DataTable.data"
          :loading="loading"
          :filter="filter"
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

    <q-page-sticky position="bottom-right" :offset="fabPos">
      <q-fab
        direction="up"
        icon="las la-calculator"
        color="brand"
        @click="calc = true"
        :disable="draggingFab"
        v-touch-pan.prevent.mouse="moveFab"
        vertical-actions-align="right"
      >
        <q-card
          style="padding:20px;border-radius:20px;"
          :disable="draggingFab"
          v-touch-pan.prevent.mouse="moveFab"
        >
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
              <td>
                <q-btn label="/" round @click="dis('/')" color="black" />
              </td>
            </tr>
            <tr>
              <td><q-btn label="4" round @click="dis('4')" /></td>
              <td><q-btn label="5" round @click="dis('5')" /></td>
              <td><q-btn label="6" round @click="dis('6')" /></td>
              <td>
                <q-btn label="-" round @click="dis('-')" color="black" />
              </td>
            </tr>
            <tr>
              <td><q-btn label="7" round @click="dis('7')" /></td>
              <td><q-btn label="8" round @click="dis('8')" /></td>
              <td><q-btn label="9" round @click="dis('9')" /></td>
              <td>
                <q-btn label="+" round @click="dis('+')" color="black" />
              </td>
            </tr>
            <tr>
              <td><q-btn label="." round @click="dis('.')" /></td>
              <td><q-btn label="0" round @click="dis('0')" /></td>
              <!-- solve function call function solve to evaluate label -->
              <td>
                <q-btn label="=" @click="solve()" round color="indigo-8" />
              </td>
              <td>
                <q-btn label="x" round @click="dis('*')" color="black" />
              </td>
            </tr>
          </table>
        </q-card>
      </q-fab>
    </q-page-sticky>
    <!-- Context Menu  -->
  </q-page>
</template>

<script>
import { Dark } from "quasar";
import VueHighcharts from "vue2-highcharts";
import * as data from "src/assets/Data.js";
import json from "src/assets/DataTable.json";
import { copyToClipboard } from "quasar";
import { exportFile } from "quasar";

function wrapCsvValue(val, formatFn) {
  let formatted = formatFn !== void 0 ? formatFn(val) : val;

  formatted =
    formatted === void 0 || formatted === null ? "" : String(formatted);

  formatted = formatted.split('"').join('""');
  /**
   * Excel accepts \n and \r in strings, but some other CSV parsers do not
   * Uncomment the next two lines to escape new lines
   */
  // .split('\n').join('\\n')
  // .split('\r').join('\\r')

  return `"${formatted}"`;
}

export default {
  name: "Home",
  components: {
    VueHighcharts
  },
  data() {
    return {
      modeicon: "las la-sun",
      pagination: "",
      Carrousel: "",
      slide: "las la-chart-area",
      text: "",
      fabPos: [18, 18],
      draggingFab: false,
      filter: "",
      loading: false,
      positionCalc: "right",
      calc: false,
      DataTable: json,
      username: "Roboto Dakasuki Mora",
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

  methods: {
    Darkmode() {
      Dark.toggle();
      if (Dark.mode == true) {
        this.modeicon = "las la-cloud-moon";
      }else{
        this.modeicon = "las la-sun";
      }
    },
    clr() {
      this.text = "";
    },
    solve() {
      this.text = eval(this.text);
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
          this.DataTable.data.map(row =>
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
