<template>
  <div class="container">
    <div class="topheadersec">
      <h2>Add a new Bill</h2>
    </div>
    <div class="billContainer">
      <div class="customerinfo">
        <div class="section1">
          <label>
            <span> Name :</span>
            <input type="text" v-model="userName" />
          </label>
          <label>
            <span>Phone no :</span>
            <input type="number" v-model="userPhone" />
          </label>
        </div>
        <div class="section2">
          <label for="">
            <span>Address :</span>
            <textarea v-model="userAddress"></textarea>
          </label>
        </div>
      </div>

      <div class="productsData">
        <div class="producttable">
          <table>
            <tr class="headItems">
              <th class="slno">SL No</th>
              <th class="item">Item Name</th>
              <th class="quanti">Quanti</th>
              <th class="rate">Rate (&#x20B9;)</th>
              <th class="amount">Amount</th>
              <th class="amount">Action</th>
            </tr>

            <tr v-for="(invoice_product, k) in invoice_products" :key="k">
              <td>{{ k + 1 }}</td>
              <td class="item">
                <input
                  type="text"
                  placeholder="Item name"
                  v-model="invoice_product.product_name"
                />
              </td>
              <td class="quanti">
                <input
                  type="number"
                  min="0"
                  step=".01"
                  placeholder="Quanti"
                  v-model="invoice_product.product_qty"
                  v-on:blur="calculateLineTotal(invoice_product)"
                />
              </td>
              <td class="rate">
                <input
                  type="number"
                  min="0"
                  step=".01"
                  placeholder="Rate"
                  v-model="invoice_product.product_price"
                  v-on:blur="calculateLineTotal(invoice_product)"
                />
              </td>
              <td class="amount">
                <span>
                  <strong> {{ invoice_product.line_total }} </strong>
                </span>
              </td>
              <td style="text-align: center">
                <button
                  class="removebtn"
                  title="Remove Item"
                  @click="deleteRow(k, invoice_product)"
                >
                  <v-icon color="red">mdi-close</v-icon>
                </button>
              </td>
            </tr>
            <tr></tr>
          </table>
        </div>
        <button class="addproductbutton" @click="addNewRow" title="Add Items">
          <v-icon color="white"> mdi-plus-circle-outline</v-icon>
        </button>
      </div>
    </div>

    <!-- Total Section  -->
    <div class="caculation">
      <div class="userNote">
        <h4>User Notes :</h4>

        <textarea
          name=""
          id=""
          v-model="userNote"
          placeholder="For example 'Thank you for your business' "
        ></textarea>
      </div>

      <div class="totalCalculation">
        <table>
          <tr>
            <td><h4>Actions</h4></td>
            <td><h3>Sub total :</h3></td>
            <td>
              <strong>&#x20B9; {{ invoice_subtotal }}/- </strong>
            </td>
          </tr>
          <tr>
            <td><span>Discount (%) : </span></td>
            <td>
              <input type="text" v-model="discount" @change="taxDisShip" />
            </td>
            <td>&#x20B9; {{ totalDiscout }}/-</td>
          </tr>
          <tr>
            <td><span>Tax (%) :</span></td>
            <td>
              <input type="text" v-model="tax" @change="taxDisShip" />
            </td>
            <td>&#x20B9; {{ totaltax }} /-</td>
          </tr>

          <tr>
            <td><span> Shipping Charge (&#x20B9;) :</span></td>
            <td>
              <input type="text" v-model="shipping" @change="taxDisShip" />
            </td>
            <td>&#x20B9; {{ shipping }} /-</td>
          </tr>
        </table>

        <div class="totalSubtotal">
          <div class="subtotalContainer">
            <div class="subtotal"></div>
            <hr />

            <div class="paymentmode">
              <span>Payment Mode :</span>
              <select name="" id="" v-model="paymentMode">
                <option value="Cash">Cash</option>
                <option value="Net Banking">Net Banking</option>
                <option value="Debit Card">Debit Card</option>
                <option value="Cradit Card">Cradit Card</option>
                <option value="UPI">UPI</option>
              </select>
            </div>

            <hr />
            <div class="total">
              <h1>Total : &#x20B9; {{ total_Amount }} /-</h1>
            </div>
          </div>
        </div>
      </div>
    </div>
    <hr />
    <div class="printbutton">
      <v-btn large @click="manu = !manu" 
      class="text-capitalize"
      
      

      color="#1365ff"
      
      >
        <v-icon>mdi-eye-outline</v-icon> &nbsp;Preview</v-btn
      >

      <v-btn large color="#ff7513" class="text-capitalize">
        <v-icon>mdi-printer</v-icon> &nbsp; Print</v-btn
      >
    </div>

    <!-- print and  preview  -->
    <v-dialog
      v-model="manu"
      close-delay="0"
      open-delay="0"
      class="red"
      @keydown.esc="manu = false"
      fullscreen
    >
      <div class="prinPreview">
        <div class="ContainerPriview">
          <div class="logoandName">
            <div class="shopLogo">
              <!-- <img src="../../assets/Logo.svg" alt="" /> -->
            </div>
            <div class="shopName"><h2>Bymond Private Limited</h2></div>

            <div class="memoNo">
              <span>Bill No : <strong>15U78</strong> </span>

              <span>Date : <strong> 20/12/21</strong> </span>
            </div>
          </div>

          <hr />

          <div class="customerDetails">
            <label>
              <span>
                Name : <strong>{{ userName }}</strong>
              </span>
            </label>
            <label>
              <span
                >Phone No : <strong> {{ userPhone }}</strong>
              </span>
            </label>
            <label>
              <span>
                Address :
                <strong>
                  {{ userAddress }}
                </strong>
              </span></label
            >
          </div>

          <div class="productDetails">
            <table>
              <tr>
                <th>SL No</th>
                <th>Item Name</th>
                <th>Quanti</th>
                <th>Rate (&#x20B9;)</th>
                <th>Amount(&#x20B9;)</th>
              </tr>
              <tr v-for="(data, idx) in invoice_products" :key="idx">
                <td>{{ idx + 1 }}</td>
                <td style="text-align: left">
                  {{ data.product_name }}
                </td>
                <td>{{ data.product_qty }}</td>
                <td>&#x20B9; {{ data.product_price }}/-</td>
                <td>&#x20B9; {{ data.line_total }}/-</td>
              </tr>
            </table>
          </div>

          <div class="totalCalculation">
            <div class="usertext">
              <span> <strong> User Note : </strong></span>
              <p>{{ userNote }}</p>
            </div>
            <div class="totalSub">
              <table>
                <tr>
                  <td>Sub Total</td>
                  <td>
                    <strong>&#x20B9; {{ invoice_subtotal }}/-</strong>
                  </td>
                </tr>
                <tr>
                  <td>
                    Discount (<strong>{{ discount }}%</strong> ) :
                  </td>
                  <td>
                    <strong>&#x20B9; {{ totalDiscout }}/-</strong>
                  </td>
                </tr>
                <tr>
                  <td>
                    Tax (<strong>{{ tax }}%</strong>) :
                  </td>
                  <td>
                    <strong>&#x20B9; {{ totaltax }}/-</strong>
                  </td>
                </tr>
                <tr>
                  <td>Shipping :</td>

                  <td>
                    <strong>&#x20B9; {{ shipping }}/-</strong>
                  </td>
                </tr>

                <tr>
                  <td><strong>Total : </strong></td>
                  <td>
                    <strong>&#x20B9; {{ total_Amount }}/-</strong>
                  </td>
                </tr>

                <tr>
                  <td>Payment Mode :</td>
                  <td>
                    <strong> {{ paymentMode }}</strong>
                  </td>
                </tr>
              </table>
            </div>
          </div>

          <hr />
          <div class="printCanButton">
            
            <div class="printbutton">
      <v-btn large @click="manu = false" 
      class="text-capitalize"
      
      

      color="red"
      
      >
         Cancle</v-btn
      >

      <v-btn large color="#ff7513" class="text-capitalize">
        <v-icon>mdi-printer</v-icon> &nbsp; Print</v-btn
      >
    </div>
          </div>
        </div>
      </div>
    </v-dialog>
  </div>
</template>

<script>
export default {
  layout: 'user',
  data() {
    return {
      invoice_subtotal: 0,
      discountData: 0,
      invoice_total: 0,
      invoice_tax: 0,
      invoice_products: [
        {
          product_no: '',
          product_name: '',
          product_price: '',
          product_qty: '',
          line_total: 0,
        },
      ],

      // discount
      discount: 0,
      totalDiscout: 0,

      //tax
      tax: 0,
      taxMode: 'persentage',
      totaltax: 0,
      // shipping charge
      shipping: 0,
      total_Amount: 0,

      // user data
      userName: null,
      userPhone: null,
      userAddress: null,
      userNote: null,
      paymentMode: 'Cash',
      // website variables

      manu: false,
    }
  },

  methods: {
    saveInvoice() {
      console.log(JSON.stringify(this.invoice_products))
    },
    calculateTotal() {
      var subtotal, total
      subtotal = this.invoice_products.reduce(function (sum, product) {
        var lineTotal = parseFloat(product.line_total)
        if (!isNaN(lineTotal)) {
          return sum + lineTotal
        }
      }, 0)
      this.invoice_subtotal = subtotal.toFixed(2)
      this.total_Amount = subtotal.toFixed(2)
      total = subtotal * (this.invoice_tax / 100) + subtotal
      total = parseFloat(total)
      if (!isNaN(total)) {
        this.invoice_total = total.toFixed(2)
      } else {
        this.invoice_total = '0.00'
      }
      this.taxDisShip()
    },
    calculateLineTotal(invoice_product) {
      var total =
        parseFloat(invoice_product.product_price) *
        parseFloat(invoice_product.product_qty)
      if (!isNaN(total)) {
        invoice_product.line_total = total.toFixed(2)
      }
      this.calculateTotal()
    },
    deleteRow(index, invoice_product) {
      var idx = this.invoice_products.indexOf(invoice_product)

      if (idx > -1) {
        this.invoice_products.splice(idx, 1)
      }
      this.calculateTotal()
      this.taxDisShip()
    },
    addNewRow() {
      this.invoice_products.push({
        product_no: '',
        product_name: '',
        product_price: '',
        product_qty: '',
        line_total: 0,
      })

      this.taxDisShip()
    },

    taxDisShip() {
      const subtotal = this.invoice_subtotal
      // total discount
      const totaldiscount = (Number(subtotal) * Number(this.discount)) / 100
      this.totalDiscout = totaldiscount.toFixed(2)

      // total tax

      const afterDiscount = Number(subtotal) - Number(totaldiscount)
      const totaltaxData = (Number(afterDiscount) * Number(this.tax)) / 100
      this.totaltax = totaltaxData.toFixed(2)

      // shippimg charge
      const shippingcharge = this.shipping
      // total amount

      const totalamount =
        Number(subtotal) -
        Number(totaldiscount) +
        Number(totaltaxData) +
        Number(shippingcharge)
      this.total_Amount = totalamount.toFixed(2)
    },
  },
}
</script>

<style lang="scss" scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.topheadersec h2 {
  color: $primary-color;
}

.container {
  padding: 0px 20px;
}
// bill container
.billContainer {
}

//  customar info

.section1 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(20rem, 49.462%));
  width: 100%;

  grid-gap: 11px;
}

.customerinfo span {
  display: block;
  color: $text-color;
  @include padding(5px, 0px, 5px, 0px);
}
.customerinfo input,
.customerinfo textarea,
.producttable input {
  width: 100%;
  @include padding(8px, 8px, 8px, 8px);
  @include border-radious(3px, 3px, 3px, 3px);
  @include border(1px, $input-border-color, solid);
  outline: none;
  font-size: 15px;
}
.customerinfo textarea {
  resize: none;
  height: 70px;
}

.scrollable-element {
  scrollbar-width: thin;
}

// product Data

.productsData {
  @include margin(2%, 0%, 0%, 0%);
}
.headItems {
  background: $primary-color;
}
.headItems th {
  color: $background-above-color;
  font-size: 14px;
  padding: 8px 6px;
}
/* bill table  */
.productsData {
  table {
    border-collapse: collapse;
    width: 100%;
  }

  td,
  th {
    border: 1px solid #dddddd;
    text-align: center;
    padding: 4px 6px;
  }
  th {
    padding: 12px 6px;
    font-size: 15px;
  }
  tr:nth-child(even) {
    background-color: #f7f7f7;
  }
}
.item {
  width: 56%;
}
.slno {
  width: 8%;
}
.quanti,
.rate,
.amount {
  width: 12%;
}
.amount {
  text-align: center;
}
.action span {
  color: $secendary-color;
}

.removebtn {
  padding: 5px;
  border: none;
  outline: none;
  background: white;
  color: red;
  border-radius: 5px;
  cursor: pointer;
}

// add product button

.addproductbutton {
  @include padding(5px, 5px, 5px, 5px);
  font-family: 'Roboto', sans-serif;
  background: $secendary-color;
  outline: none;
  border: none;
  @include border-radious(5px, 5px, 5px, 5px);
  font-weight: 500;
  cursor: pointer;
  color: $background-above-color;
  display: flex;
  justify-content: center;
  font-size: 16px;
  @include margin(0.5%, 0%, 0%, 0%);
}

// total Section

.totalSec {
  @include margin(4%, 0%, 0%, 0%);
  float: right;
  span {
    padding: 2px 0px;
    font-size: 18px;
  }
}

.aditionalbuttons {
  @include margin(1%, 0%, 0%, 0%);

  .dicountbtn,
  .taxtbtn,
  .shipingbtn {
    @extend .addproductbutton;
    display: inline;
    font-size: 14px;
    padding: 8px;
  }

  .active {
    color: white;
  }

  span {
    font-size: 10px;
  }
}
// total Section
.caculation {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  margin-top: 50px;
  span {
    display: inline;
    color: $text-color;
    @include padding(5px, 0px, 5px, 0px);
  }

  .userNote {
    padding: 8px 20px 0px 0px;
  }
  textarea {
    width: 100%;
    height: 160px;
    resize: none;
    margin-top: 13px;

    outline: none;

    @include padding(8px, 8px, 8px, 8px);
    @include border-radious(3px, 3px, 3px, 3px);
    @include border(1px, $input-border-color, solid);
    outline: none;
    font-size: 15px;
  }

  .totalSubtotal {
    width: 100%;
  }

  .subtotalContainer {
    width: fit-content;
    float: right;

    padding: 30px 0px 30px 0px;
  }

  table {
    border-collapse: collapse;
    width: 100%;
  }

  td,
  th {
    @include border(1px, $input-border-color, solid);
    text-align: center;
    @include padding(8px, 8px, 8px, 8px);
  }
  th {
    padding: 8px 4px;
  }

  tr:nth-child(even) {
    background-color: #f7f7f7;
  }

  input {
    width: 80px;
    @include padding(8px, 8px, 8px, 8px);
    @include border-radious(3px, 3px, 3px, 3px);
    @include border(1px, $input-border-color, solid);
    outline: none;
    font-size: 15px;
    display: inline;
  }

  select {
    padding: 5px 5px;
    outline: none;
    @include border(1px, $input-border-color, solid);
    cursor: pointer;
    font-size: 17px;
  }
  hr {
    border-top: 1px $secendary-color solid;
    margin: 20px 0px;
  }
}

// action buttons

.printbutton {
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;

  button {
    padding: 10px 25px;
    margin: 0px 10px;
    font-size: 17px;
    border-radius: 5px;
    outline: none;
    border: none;
    color: white;
    font-weight: 500;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    letter-spacing: 0.01rem;
  }
  .previewbtn {
    background: $primary-color;
  }
  .printbtn {
    background: $secendary-color;
  }
}
hr {
  border-top: 1px $secendary-color solid;
  margin: 20px 0px;
}

// print priview

.prinPreview {
  position: fixed;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.466);
  display: flex;
  justify-content: center;
  overflow: auto;

  .ContainerPriview {
    background: white;
    padding: 30px 35px;
    width: 60vw;
    height: fit-content;
    border-radius: 6px;
    margin-top: 5vh;
    margin-bottom: 10vh;
  }
  .logoandName {
    display: flex;

    align-items: center;

    .shopLogo {
      text-align: left;
      width: 15%;
    }
    .shopName {
      width: 65%;
      text-align: center;
    }
    .shopName h2 {
      font-size: 30px;
      color: $primary-color;
      font-weight: 900;
      font-family: 'Roboto', sans-serif;
    }

    .memoNo {
      width: 20%;

      text-align: right;
    }

    .memoNo span {
      font-size: 15px;
      display: block;
      margin: 5px 0px;
    }

    img {
      width: 100%;
    }
  }

  hr {
    border-top: 1px rgb(161, 161, 161) solid;
    margin: 20px 0px;
  }
  .customerDetails span strong {
    font-size: 18px;
    font-weight: 500;
  }
  label {
    display: block;
    margin: 3px 0px;
  }
  .productDetails {
    margin-top: 15px;
  }

  table {
    border-collapse: collapse;
    width: 100%;
  }

  td,
  th {
    @include border(1px, rgb(190, 190, 190), solid);
    text-align: center;
    @include padding(6px, 6px, 6px, 6px);
  }
  th {
    color: $primary-color;
  }

  tr:nth-child(even) {
    background-color: #fcfcfc;
  }

  .totalCalculation {
    margin-top: 10px;
    display: flex;
  }

  .usertext {
    width: 60%;
  }
  .totalSub {
    width: 40%;
  }

  .printCanButton {
    text-align: right;
  
    display: flex;
    justify-content: center;
    float: right;
  }
  .printCanButton button {
    padding: 10px 25px;
    margin: 0px 5px;
    font-size: 17px;
    border-radius: 5px;
    outline: none;
    border: none;
    color: white;
    font-weight: 500;
    cursor: pointer;
  }
  .print {
    background: $primary-color;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .cancle {
    background: red;
  }
  p {
    margin-top: 10px;
  }
}
</style>
