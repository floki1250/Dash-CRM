<template>
  <q-page class="flex page">
    <div
      class="row justify-between fluent"
      style="padding-top: 5px;width:100%;height:fit-content;"
    >
      <div class="overview text">Overview</div>
      <q-dialog v-model="searchbar">
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
          <q-popup-edit :cover="false" style="background:transparent">
            <div style="height: 200px; width:150px">
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
        <q-separator vertical />
        <div class="row" style="margin:2px">
          <p style="padding: 10px 2px 0px 0px" class="text">{{ username }}</p>

          <q-avatar size="40px" @click="refresh" >
            <img src="~/assets/avatar.png" alt="" />
          </q-avatar>
        </div>
      </div>
    </div>

    <div
      class="row"
      style="width: 100%;
               height: 100%;
               margin-top:0%;
               display: flex;
               "

    >
      <div
        class="widget fluent"
        onclick="()';"
        style="cursor: pointer;  width:30% ;"
      ></div>
      <div
        class="widget fluent"
        onclick="refresh()"
        style="cursor: pointer; width:30%"
      >
        Hello world!
      </div>
      <div class="widget fluent" onclick="()';" style="cursor: pointer; ">
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
        @click="refresh"
        style="cursor: pointer; height:400px ;min-width:400px;flex:2; "
      >
        <vue-highcharts
          :options="areaOptions"
          ref="areaCharts"
        ></vue-highcharts>
      </div>

      <div
        class="widget fluent"
        onclick="()';"
        style="cursor: pointer; height:400px ; flex:1 ;"
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
      <div class="widget fluent" style="padding:10px;width:100%;">
        <q-table
          title="Treats"
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
        />
      </div>
    </div>
  </q-page>
</template>

<script>
import VueHighcharts from "vue2-highcharts";
import * as data from "src/assets/Data.js";
import json from "src/assets/DataTable.json"

export default {
  name: "Home",
  components: {
    VueHighcharts
  },
  data() {
    return {
      inputTextSearch:"",
      DataTable:json,
      username: "Roboto Dakasuki Mora",
      searchbar: false,
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
    };
  },

  mounted() {},
  methods: {
    refresh:function(){
     var x =document.getElementByClassName('highcharts-container ').innerHTML;
     document.getElementByClassName('highcharts-container ').innerHTML=x;
    },
    scrolled(position) {
      // when this method is invoked then it means user
      // has scrolled the page to `position`
      //
      // `position` is an Integer designating the current
      // scroll position in pixels.
    },
    showNotif(position) {
      setTimeout(() => {
        this.$q.notify({
          message: "Hello World!",
          color: "blue",
          position,
          progress: true,
        });
      }, 50);
    }
  }
};
</script>
