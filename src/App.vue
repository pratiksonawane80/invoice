<template>
  <div class="invoice-box">
    <div class="invoice-drawline"></div>
    <div class="invoice-company-info">
      <div id="invoice-company-left">
        <span class="invoice-company-name">Jonathan Doughertty</span>
        <br />
        <span class="invoice-company-address">
          1950, N.Pleasant Street,
          <br />
          Lorem Ipsum, Dolor sit amet, Consectetur, Tempor(E) <br />Mumbai
          -400072, Maharashtra
        </span>
      </div>
      <div id="invoice-company-right">
        <span class="invoice-info">Invoice</span>
        <span class="invoice-date">Submitted &emsp; 25 Oct 1993</span>
      </div>
    </div>

    <div class="invoice-user-info">
      <div id="invoice-company-left">
        <span class="invoice-for" style="margin-left: 5px">Invoice for</span>
        <br />
        <div class="address-manage">
          <div style="margin-left: 5px">
            <span
              class="invoice-company-address"
              style="line-height: 1.4 !important"
            >
              Awesome Services India Pvt. Ltd.
              <br />
              Lorem Ipsum, Dolores, 49 Tempor Road <br />
              Dolore eu fugiat nulla priatur. SC (W) <br />
              Mumbai - 400054, Maharsshtra
            </span>
          </div>
        </div>
      </div>
      <div
        id="invoice-company-right"
        style="
          line-height: 1 !important;
          float: right;
          text-align: right;
          padding-top: 30px;
        "
      >
        <span class="invoice-for">Payable to :</span>
        <span>Pranshu Sharma</span>
        <br />
        <span class="invoice-for">Invoice # :</span>
        <span style="margin-right: 17%">10003</span>
        <br />
        <span class="invoice-for">Invoice date :</span>
        <span style="margin-right: 6%">30 Sep 2017</span>
        <br />
      </div>
    </div>

    <hr class="invoice-drawline-thin" />

    <table cellpadding="0" cellspacing="0">
      <tr class="heading">
        <td>
          Description
          <button @click="sortbyDesc(), (ascending = !ascending)"><i class="arrow" :class="(isActiveArrow)?'up_arrow':'down_arrow'"></i></button>
        </td>
        <td>
          Qty
          <button @click="sortByQty(), (ascending = !ascending)"><i class="arrow" :class="(isActiveArrow)?'up_arrow':'down_arrow'"></i></button>
        </td>
        <td>
          Rate
          <button @click="sortByRate(), (ascending = !ascending)"><i class="arrow" :class="(isActiveArrow)?'up_arrow':'down_arrow'"></i></button>
        </td>
        <td>
          Total price
          <button @click="sortByTotal(), (ascending = !ascending)"><i class="arrow" :class="(isActiveArrow)?'up_arrow':'down_arrow'"></i></button>
        </td>
        <td id="toggle_removal">
          <button @click="toggleDisable()">Disable</button>
          
        </td>
      </tr>

      <tr
        :class="{ even_row: index % 2 }"
        class="item"
        v-for="(arr, index) in array"
        :key="arr.id"
      >
        <td>{{ arr.description }}</td>
        <td>{{ arr.qty }}</td>
        <td>&#x20b9;{{ arr.rate }}</td>
        <td>&#x20b9;{{ arr.totalPrice }}</td>
        <td>
          <button
            class="crossbtn"
            :class="{ disableBtn: isDisable }"
            @click="removeEntry(index)"
          >
            x
          </button>
        </td>
      </tr>

      <tr class="item" style="height: 33px">
        <td colspan="4"></td>
      </tr>
      <tr class="item" style="height: 33px">
        <td
          colspan="4"
          style="border-bottom: 1px solid rgb(226, 218, 218)"
        ></td>
      </tr>

      <tr class="item">
        <td>
          <span style="color: gray; font-weight: 1000">Notes</span>
        </td>
        <td colspan="2" style="color: #2c3d99">Subtotal</td>
        <td>
          <span style="font-weight: 1000">&#x20b9;{{ totalOfInvoice }} </span>
        </td>
      </tr>
    </table>

    <div class="subtotal">
      <span style="text-align: right">&#x20b9;{{ totalOfInvoice }}</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num: 1,
      ascending: true,
      finalTotal: 0,
      isActiveArrow: true,
      array: [
        {
          id: 1,
          description: "dolore eu fuglat nulla parlatur",
          qty: "20",
          rate: "1000.00",
          totalPrice: "20000.0",
        },
        {
          id: 2,
          description: "sed do elusmod tempor incididunt",
          qty: "3",
          rate: "243.00",
          totalPrice: "721.0",
        },
        {
          id: 3,
          description: "item 123",
          qty: "20",
          rate: "1000.00",
          totalPrice: "21000.0",
        },
        {
          id: 4,
          description: "AYItem XYZ",
          qty: "3",
          rate: "2430.00",
          totalPrice: "7210.0",
        },
        {
          id: 5,
          description: "nulla parlatu",
          qty: "20",
          rate: "100.00",
          totalPrice: "2000.0",
        },
        {
          id: 6,
          description: "AY",
          qty: "3",
          rate: "2243.00",
          totalPrice: "6729.0",
        },
        {
          id: 7,
          description: "dolore eu fuglat nulla parlatur",
          qty: "20",
          rate: "1000.00",
          totalPrice: "20000.0",
        },
        {
          id: 8,
          description: "sed do elusmod tempor incididunt",
          qty: "3",
          rate: "243.00",
          totalPrice: "721.0",
        },
        {
          id: 9,
          description: "incididunt tempor incididun nulla",
          qty: "17",
          rate: "1100.00",
          totalPrice: "18700.0",
        },
        {
          id: 10,
          description: "sed do elusmod tempor incididunt",
          qty: "3",
          rate: "243.00",
          totalPrice: "721.0",
        },
        {
          id: 11,
          description: "lorem ipsum dolor set amet tempor dolor ameu dolore eu fuglat nulla parlatur",
          qty: "9",
          rate: "10.00",
          totalPrice: "90.0",
        },
        {
          id: 12,
          description: "sed do elusmod tempor incididunt",
          qty: "3",
          rate: "243.00",
          totalPrice: "721.0",
        },
        {
          id: 13,
          description: "Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatu",
          qty: "11",
          rate: "196.24",
          totalPrice: "2158.6",
        },
        {
          id: 14,
          description: "abcdef test item",
          qty: "3",
          rate: "12.00",
          totalPrice: "36",
        },
        {
          id: 15,
          description: "U corporis suscipit laboriosam, nisi ut aliquid",
          qty: "11",
          rate: "196.24",
          totalPrice: "2158.6",
        },
        {
          id: 16,
          description: "abcdef test item",
          qty: "30",
          rate: "120.00",
          totalPrice: "3600.0",
        },
      ],
      isDisable: false,
    };
  },

  computed: {
    totalOfInvoice() {
      let total = this.array.reduce((acc, ele) => {
        return acc + parseInt(ele.totalPrice);
      }, 0);

      return total;
    },
  },

  methods: {
    changeClass() {
      this.isActiveArrow = !this.isActiveArrow
    },
    toggleDisable() {
      this.isDisable = !this.isDisable;
      console.log(this.isDisable);
    },
    sortbyDesc() {
      let ascAlpha = this.array;

      ascAlpha = ascAlpha.sort((a, b) => {
        let a1 = a.description.toLowerCase(),
          b1 = b.description.toLowerCase();

        if (a1 < b1) {
          return -1;
        }
        if (a1 > b1) {
          return 1;
        }
        return 0;
      });
      if (!this.ascending) {
        ascAlpha.reverse();
      }
      this.changeClass()
      return ascAlpha;
    },

    sortByQty() {
      let ascQty = this.array;

      ascQty = ascQty.sort((a, b) => {
        return a.qty - b.qty;
      });
      if (!this.ascending) {
        ascQty.reverse();
      }
      this.changeClass()
      return ascQty;
    },

    sortByRate() {
      let ascRate = this.array;

      ascRate = ascRate.sort((a, b) => {
        return a.rate - b.rate;
      });
      if (!this.ascending) {
        ascRate.reverse();
      }
      this.changeClass()
      return ascRate;
    },

    sortByTotal() {
      let ascTotal = this.array;

      ascTotal = ascTotal.sort((a, b) => {
        return a.totalPrice - b.totalPrice;
      });
      if (!this.ascending) {
        ascTotal.reverse();
      }
      this.changeClass()
      return ascTotal;
    },

    removeEntry(index) {
      this.array.splice(index, 1);
    },
  },
};
</script>

<style>
html,
body {
  margin: 1%;
}

.invoice-drawline {
  width: 100%;
  height: 10px;
  background-color: #243085;
}

.invoice-drawline-thin {
  margin: 4%;
  background-color: #f3f3f3;
  position: relative;
  margin-top: 365px;
  display: block;
  clear: both;
}

.invoice-company-info {
  background-color: aqua;
  height: auto;
  margin: 4%;
  position: relative;
}

#invoice-company-left {
  float: left;
  width: 65%;
  background-color: #fff;
}

#invoice-company-right {
  float: left;
  width: 35%;
  background-color: #fff;
}

.invoice-company-name {
  color: #6f66e8;
  font-size: 26px;
  font-weight: 550;
  font-family: "Lato", sans-serif;
}

.invoice-info {
  color: #2c3d99;
  font-size: 45px;
  width: 100%;
  font-weight: 1000;
  float: right;
  text-align: right;
  margin-bottom: 13px;
}

.subtotal {
  color: #e01b87;
  font-size: 26px;
  font-weight: 1000;
  font-family: "Lato", sans-serif;
  width: 92%;
  margin: 4%;
  text-align: right;
}

.invoice-date {
  color: #e01b87;
  font-size: 17px;
  font-weight: bold;
  float: right;
  text-align: right;
  margin-top: 20px;
  font-family: "Lato", sans-serif;
}

.invoice-company-address {
  font-family: "Lato", sans-serif;
}

.address-manage {
  background-color: #f3f3f3;
  width: 50%;
}

.invoice-user-info {
  margin-left: 4%;
  margin-right: 4%;
  margin-top: 220px;
  position: relative;
}

.invoice-for {
  font-family: bold;
  font-size: 17px;
  font-weight: 900;
  line-height: 28px;
  margin-top: 30px;
}

td {
  font-family: "Lato", sans-serif;
}

.invoice-box {
  max-width: auto;
  margin: auto;
  padding: 30px;
  border: 1px solid #eee;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
  font-size: 16px;
  line-height: 24px;
  font-family: "Lato", sans-serif;
}

@media only screen and (max-width: 280px) {
  .invoice-user-info {
    margin-left: 4%;
    margin-right: 4%;
    margin-top: 500px;
    position: relative;
  }
}

@media only screen and (max-width: 600px) {
  .invoice-drawline-thin {
    margin: 4%;
    height: 1px;
    background-color: gray;
    position: relative;
    margin-top: 400px;
  }
  .address-manage {
    background-color: #f3f3f3;
    width: 90%;
  }
  .invoice-company-name {
    color: #6f66e8;
    font-size: 18px;
    font-weight: 550;
    font-family: "Lato", sans-serif;
  }
  .invoice-box table tr.top table td {
    width: 100%;
    display: block;
    text-align: center;
  }
  .invoice-box table tr.information table td {
    width: 100%;
    display: block;
    text-align: center;
  }
  .invoice-info {
    color: #2c3d99;
    font-size: 30px;
    width: 100%;
    font-weight: 1000;
    float: right;
    text-align: right;
    margin-bottom: 13px;
  }
  .invoice-date {
    color: #e01b87;
    font-size: 13px;
    font-weight: bold;
    float: right;
    text-align: right;
    margin-top: 20px;
    font-family: "Lato", sans-serif;
  }
}

.invoice-box table {
  width: 92%;
  line-height: inherit;
  text-align: right;
  margin: 4%;
}

.invoice-box table td {
  padding: 5px;
  vertical-align: top;
}

.invoice-box table tr.top table td {
  padding-bottom: 20px;
}

.invoice-box table tr.top table td.title {
  font-size: 45px;
  line-height: 45px;
  color: #333;
}

.invoice-box table tr.information table td {
  padding-bottom: 40px;
}

.invoice-box table tr.heading td {
  border-bottom: none;
  color: #2c3d99;
  font-weight: bold;
}

.invoice-box table tr.heading td:first-child {
  text-align: left !important;
}

.invoice-box table tr.item td:first-child {
  text-align: left !important;
  width: 60%;
}

.invoice-box table tr.item td {
  vertical-align: middle;
}

.even_row {
  background-color: #f3f3f3;
}

.cross {
  font-size: 12px;
  color: red;
}

.crossbtn {
  border-radius: 5px;
  background-color: lightgreen;
}

.disableBtn {
  pointer-events: none;
  background-color: red;
}

.arrow {
  border: solid black;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
}
.up_arrow {
  transform: rotate(-135deg);
  -webkit-transform: rotate(-135deg);
}
.down_arrow {
  transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
}

/** RTL **/

.rtl {
  direction: rtl;
  font-family: Tahoma, "Helvetica Neue", "Helvetica", Helvetica, Arial,
    sans-serif;
}

.rtl table {
  text-align: right;
}

.rtl table tr td:nth-child(2) {
  text-align: right;
}
</style>
