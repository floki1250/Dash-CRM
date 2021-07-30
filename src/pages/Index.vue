<template>
  <q-page class="flex page">
    <div class="popup">
      <q-icon name="las la-exclamation-triangle" /> Enlarge window screen for
      better visibility !
    </div>
    <div class="row justify-between light headerBar">
      <div class="overview text">Overview</div>

      <div class="row" style="position:absolute;right:1%;">
        <div>
          <q-btn color="grey" :icon="modeicon" flat round @click="Darkmode" />
        </div>
        <div>
          <q-btn color="grey" icon="las la-bell" flat round
            ><q-badge floating color="red" transparent rounded
              >+9</q-badge
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
        <div
          class="vl"
          style="border-left: 1px solid grey;
  height: 40px;margin:2px 20px 2px 20px"
        ></div>
        <div class="row">
          <p class="text username">
            {{ username }}
          </p>

          <q-avatar size="40px">
            <img src="../assets/avatar.png" alt="" />
          </q-avatar>
        </div>
      </div>
    </div>
    <div class="row grid">
      <div style="flex:0.7;">
        <div
          class=" widget fluent"
          onclick="()';"
          style="cursor: pointer;width:250px "
        >
          <Clock style="padding:10%;width:100%" />
        </div>
        <div
          class="widget fluent"
          onclick="()';"
          style="cursor: pointer;  width:250px ; height:65%"
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
              class="column no-wrap flex-center q-carousel-slide"
            >
              <q-icon size="56px"
                ><img src="../assets/growth.svg" alt="" class="Carrousel-Icon"
              /></q-icon>
              <div class="q-mt-md text-center">
                Revenue Increased By 5% this Month
              </div>
            </q-carousel-slide>
            <q-carousel-slide
              name="las la-chart-bar"
              class="column no-wrap flex-center q-carousel-slide"
            >
              <q-icon size="56px"
                ><img src="../assets/decrease.svg" alt="" class="Carrousel-Icon"
              /></q-icon>
              <div class="q-mt-md text-center">
                Lost 500$ this Week
              </div>
            </q-carousel-slide>
            <q-carousel-slide
              name="las la-project-diagram"
              class="column no-wrap flex-center q-carousel-slide"
            >
              <q-icon size="56px"
                ><img src="../assets/bank.svg" alt="" class="Carrousel-Icon"
              /></q-icon>
              <div class="q-mt-md text-center">
                Added 1000$ To the Bank
              </div>
            </q-carousel-slide>
            <q-carousel-slide
              name="las la-chart-line"
              class="column no-wrap flex-center q-carousel-slide"
            >
              <q-icon size="56px"
                ><img
                  src="../assets/balance.svg"
                  srcset=""
                  alt=""
                  class="Carrousel-Icon"
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
        <v-chart class="chart" :option="option" :autoresize="autoresize" />
      </div>

      <div
        class="widget fluent"
        onclick="()';"
        style="cursor: pointer; height:400px ; flex:0.5 ;"
      >
        <p class="product">Top Product</p>

        <q-scroll-area style="width: 100%; height: 75%;overflow: hidden ;">
          <div v-for="i in 50" :key="i" class="product-item row">
            <div>
              <q-icon> <img src="../assets/smartwatch.png"/></q-icon>
            </div>
            <div style="margin-left:10px">Smartwatch {{ i }}</div>
            <div style="margin-right:1px;margin-left:10px;font-weight: 500;">
              500$
            </div>
          </div>
        </q-scroll-area>
      </div>
      <div class="widget fluent" style="padding:10px;width:100%;">
        <q-table
          title="Test"
          :columns="columns"
          row-key="productId"
          selection="multiple"
          :selected.sync="selected"
          color="#e4e4e4d2"
          card-class="#e4e4e4d2"
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
              <q-item-section no-caps
                ><div class="row">
                  <q-icon
                    name="las la-file-export"
                    size="sm"
                    style="padding-right:5px"
                  />
                  <JsonExcel
                    :data="DataTable.data"
                    :name="file"
                  ></JsonExcel></div
              ></q-item-section>
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

import json from "src/assets/DataTable.json";
import ChartData from "src/assets/ChartData.json";
import { copyToClipboard } from "quasar";
import Clock from "app/component/clock.vue";
import { use } from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { BarChart } from "echarts/charts";
import JsonExcel from "vue-json-excel";
import { GridComponent, TooltipComponent } from "echarts/components";
import VChart, { THEME_KEY } from "vue-echarts";
var tot =(function calculate_Totals(json){
  for (var i = 0; i < json.length;i++) {
     tot = total(json[i].productSalePrice);
  }
 return tot;
});
use([CanvasRenderer, BarChart, GridComponent, TooltipComponent]);

const today = new Date();
const filename =
  "Export-" +
  today.getDate() +
  "-" +
  eval(today.getMonth() + 1) +
  "-" +
  today.getFullYear() +
  ".xls";
export default {
  provide: {
    [THEME_KEY]: "light"
  },
  name: "Home",
  components: {
    Clock,
    VChart,
    JsonExcel
  },
  data() {
    return {
      totalRev : tot,
      file: filename,
      autoresize: true,
      textTable: "text-white-8",
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
      username: "Adem Dardour",
      option: {
        color: ["#3398DB"],
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "shadow"
          }
        },
        grid: {},
        xAxis: [
          {
            type: "category",
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
            axisTick: {
              alignWithLabel: true
            }
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: [
          {
            name: "Sales",
            type: "bar",
            barWidth: "50%",
            data: ChartData.data
          }
        ],

        animationDuration: 500
      },

      selected: [],
      columns: [
        {
          name: "Id",
          required: true,
          label: "product Id",
          align: "center",
          field: "productId",
          sortable: true
        },
        {
          name: "product Name",
          align: "left",
          label: "productName",
          field: "productName",
          sortable: true
        },
        {
          name: "productStock",
          label: "Stock",
          field: "productStock",
          sortable: true
        },
        {
          name: "productPrice",
          label: "$ Price",
          field: "productPrice",
          sortable: true
        },
        {
          name: "productSalePrice",
          label: "Sale Price",
          field: "productSalePrice"
        },
        {
          name: "rating",
          label: "rating",
          field: "rating",
          sortable: true,
          align: "left"
        }
      ]
    };
  },

  methods: {
    Darkmode() {
      Dark.toggle();
      if (Dark.mode == true) {
        this.modeicon = "las la-cloud-moon";
        this.textTable = "text-white-8";
      } else {
        this.modeicon = "las la-sun";
        this.textTable = "text-black-8";
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
    getSelectedString() {
      return this.selected.length === 0
        ? ""
        : `${this.selected.length} record${
            this.selected.length > 1 ? "s" : ""
          } selected of ${this.data.length}`;
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
  }
};
</script>
