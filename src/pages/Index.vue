<template>
  <q-page class="flex" style="background-color: rgb(230, 230, 230);display: table;">
    <div class="row justify-between" style="padding-top: 5px;">
      <div class="overview text">Overview</div>
      <q-dialog v-model="searchbar">
        <div style="background-color: rgb(230, 230, 230);">
          <q-input
            bottom-slots
            v-model="text"
            style="width:500px"
            :dense="true"
            clearable
            standout
            bg-color="grey-6"
            autofocus
          >
            <template v-slot:prepend>
              <q-icon name="las la-search" />
            </template>
          </q-input>
          <div>
            <q-scroll-area style="height: 200px;">
              <div v-for="n in 50" :key="n">
                <q-item clickable> Result N°{{ n }} </q-item>
              </div>
            </q-scroll-area>
          </div>
        </div>
      </q-dialog>
      <div class="row" style="position:absolute;right:2%;">
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
          <q-popup-edit :cover="false">
            <div>
              <q-scroll-area style="height: 200px; width:150px">
                <q-item clickable v-for="i in 10" :key="i">Message {{ i }}</q-item>
              </q-scroll-area>
            </div>
          </q-popup-edit>
        </div>
        <q-separator vertical />
        <div class="row" style="margin:5px">
          <p style="padding: 10px 5px 0px 0px" class="text">{{username}}</p>
          <q-avatar><img src="~/assets/avatar.png" alt=""/></q-avatar>
        </div>
      </div>
    </div>

    <div
      class="row"
      style="background-color: rgb(230, 230, 230);
               width: 100%;
               height: 100%;
               margin-top:0%;"
    >
      <div class="widget" onclick="()';" style="cursor: pointer;  width:30%">
        Hello World!
      </div>
      <div class="widget" onclick="()';" style="cursor: pointer; width:30%">
        Hello world!
      </div>
      <div class="widget" onclick="()';" style="cursor: pointer; ">
        <iframe
          src="https://free.timeanddate.com/clock/i7untxj0/n253/fn16/fs30/tct/pct/pa9/tt0/tw0/tm1/td2/th1/tb4"
          frameborder="0"
          width="100%"
          height="88"
          allowtransparency="true"
        ></iframe>
      </div>
     
      <div
        class="widget"
        onclick="()';"
        style="cursor: pointer; height:400px ; width:60%; "
      >
        <vue-highcharts
          :options="areaOptions"
          ref="areaCharts"
        ></vue-highcharts>
      </div>
      
      <div
        class="widget"
        onclick="()';"
        style="cursor: pointer; height:400px ; width:35% ;"
      >
        <q-scroll-area
          style="width:100%;text-align:center;padding:20px 0px 0px 0px;"
        >
          <div>
            <q-separator />
            <p>Top Selling Product</p>
            <div>
              <p>Samsung S21</p>
              <p>55555 $</p>
            </div>
          </div>
          <q-separator />
          <div>
            <p>least Selling Product</p>
            <q-icon name="top" />
          </div>
        </q-scroll-area>
      </div>
      <div class="widget" style="padding:10px;width:100%;">
        <q-table
          title="Treats"
          :data="data"
          :columns="columns"
          row-key="name"
          selection="single"
          :selected.sync="selected"
          color="#e4e4e4d2"
          card-class="#e4e4e4d2"
          table-class="text-grey-8"
          table-header-class="text-black"
          style="width:100%"
        />
      </div>
    </div>
  </q-page>
</template>

<script>
import VueHighcharts from "vue2-highcharts";
import * as data from "src/assets/Data.js";
export default {
  name: "Home",
  components: {
    VueHighcharts
  },
  data() {
    return {
      username: "Roboto Dakasuki Mora",
      searchbar: false,
      text: "",
      thumbStyle: {
        right: "4px",
        borderRadius: "5px",
        backgroundColor: "#027be3",
        width: "5px",
        opacity: 0.75
      },

      barStyle: {
        right: "2px",
        borderRadius: "9px",
        backgroundColor: "#027be3",
        width: "9px",
        opacity: 0.2
      },
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
      ],
      data: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          sodium: 87,
          calcium: "14%",
          iron: "1%"
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          sodium: 129,
          calcium: "8%",
          iron: "1%"
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          sodium: 337,
          calcium: "6%",
          iron: "7%"
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          sodium: 413,
          calcium: "3%",
          iron: "8%"
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          sodium: 327,
          calcium: "7%",
          iron: "16%"
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          sodium: 50,
          calcium: "0%",
          iron: "0%"
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          sodium: 38,
          calcium: "0%",
          iron: "2%"
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          sodium: 562,
          calcium: "0%",
          iron: "45%"
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          sodium: 326,
          calcium: "2%",
          iron: "22%"
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          sodium: 54,
          calcium: "12%",
          iron: "6%"
        }
      ]
    };
  },
  mounted() {},
  methods: {
    scrolled(position) {
      // when this method is invoked then it means user
      // has scrolled the page to `position`
      //
      // `position` is an Integer designating the current
      // scroll position in pixels.
    }
  }
};
</script>
